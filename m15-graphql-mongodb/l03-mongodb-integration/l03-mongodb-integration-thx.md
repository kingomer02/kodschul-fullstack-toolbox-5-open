# Modul 15: GraphQL und MongoDB

## Lab 15.3 - MongoDB-Integration für TeamBoard

---

## Lab-Ziel

Du bindest den offiziellen MongoDB-Treiber ins Backend ein, ersetzt die In-Memory-Speicherung durch eine echte MongoDB-Collection und ergänzt ein GraphQL-Schema für Tickets neben der bestehenden REST-API.

**Leitfragen:**

<details>
<summary>Reicht es, nur `TicketRepository` auf MongoDB umzustellen?</summary>

Fast. Die **Fachlogik** im `TicketService` bleibt gleich - die Reihenfolge `To Do → In Progress → Done` ändert sich nicht. Zwei Dinge schlagen aber durch:

1. **Alles wird `async`.** Datenbankzugriffe laufen nie synchron. Sobald das Repository `Promise`s zurückgibt, muss der Service `await` schreiben - und jede Route auch. "async ist ansteckend."
2. **Ändern heißt jetzt Speichern.** Bisher hat der Service das Ticket-Objekt im Speicher verändert, und das war die Änderung. Mit MongoDB ist das gelesene Objekt nur eine **Kopie** - ohne ausdrückliches `update` geht der neue Status beim nächsten Lesen verloren.

</details>

<details>
<summary>Warum laufen REST und GraphQL im selben Backend-Prozess nebeneinander, statt getrennte Server zu sein?</summary>

`@apollo/server` mit `@as-integrations/express4` lässt sich als zusätzliche Middleware in eine bestehende Express-App einhängen - beide APIs teilen sich denselben Prozess, Port und Datenzugriff über `TicketRepository`.

</details>

---

## MongoDB-Treiber einbinden

```bash
cd backend
npm install mongodb @apollo/server @as-integrations/express4 graphql graphql-tag
```

```ts
// backend/src/repositories/ticket-repository.ts
import { Collection, MongoClient } from "mongodb";
import { Ticket } from "../models/ticket";

// MongoDB legt ein eigenes Feld _id an - nach außen geben wir es nicht heraus
const withoutId = { projection: { _id: 0 } };

export class TicketRepository {
  private collection!: Collection<Ticket>;

  async connect(url: string): Promise<void> {
    const client = new MongoClient(url);
    await client.connect();
    this.collection = client.db().collection<Ticket>("tickets");
    console.log("Connected to MongoDB");
  }

  async add(ticket: Ticket): Promise<void> {
    // Kopie: insertOne hängt sonst _id an unser Objekt
    await this.collection.insertOne({ ...ticket });
  }

  async findById(id: string): Promise<Ticket | undefined> {
    return (await this.collection.findOne({ id }, withoutId)) ?? undefined;
  }

  async getAll(): Promise<Ticket[]> {
    return this.collection.find({}, withoutId).toArray();
  }

  async update(ticket: Ticket): Promise<void> {
    await this.collection.updateOne({ id: ticket.id }, { $set: { ...ticket } });
  }

  async count(): Promise<number> {
    return this.collection.countDocuments();
  }
}
```

- Alle Methoden werden `async`, weil Datenbankzugriffe nie synchron ablaufen.
- `private collection!:` - das `!` sagt dem Compiler: "wird gesetzt, bevor es benutzt wird" (in `connect`).
- `update` ist neu: Änderungen müssen ausdrücklich zurückgeschrieben werden.

---

## Der Service speichert jetzt selbst

```ts
// backend/src/services/ticket-service.ts
import { Ticket } from "../models/ticket";
import { TicketRepository } from "../repositories/ticket-repository";

export class TicketService {
  constructor(private repository: TicketRepository) {}

  async moveToNextStatus(id: string): Promise<Ticket | undefined> {
    const ticket = await this.repository.findById(id);
    if (!ticket) return undefined;

    const order: Ticket["status"][] = ["To Do", "In Progress", "Done"];
    const nextIndex = Math.min(order.indexOf(ticket.status) + 1, order.length - 1);
    ticket.status = order[nextIndex];
    await this.repository.update(ticket); // neu: zurück in die Datenbank
    return ticket;
  }

  async assign(id: string, assignee: string): Promise<Ticket | undefined> {
    const ticket = await this.repository.findById(id);
    if (!ticket) return undefined;
    ticket.assignee = assignee;
    await this.repository.update(ticket);
    return ticket;
  }
}
```

Die Statuslogik selbst - die Reihenfolge und das Stehenbleiben bei `Done` - ist **unverändert**. Genau dafür wurden Repository und Service in Modul 8 getrennt.

---

## GraphQL-Schema für Tickets

```ts
// backend/src/graphql/schema.ts
import gql from "graphql-tag";
import { Ticket } from "../models/ticket";
import { TicketRepository } from "../repositories/ticket-repository";

export const typeDefs = gql`
  type Ticket {
    id: ID!
    title: String!
    description: String!
    assignee: String!
    status: String!
  }

  type Query {
    tickets: [Ticket!]!
  }

  type Mutation {
    createTicket(title: String!, description: String, assignee: String): Ticket!
  }
`;

export const createResolvers = (repository: TicketRepository) => ({
  Query: {
    tickets: () => repository.getAll(),
  },
  Mutation: {
    createTicket: async (
      _: unknown,
      args: { title: string; description?: string; assignee?: string }
    ): Promise<Ticket> => {
      const ticket: Ticket = {
        id: `t-${Date.now()}`,
        title: args.title,
        description: args.description ?? "",
        assignee: args.assignee ?? "",
        status: "To Do",
      };
      await repository.add(ticket); // await: sonst antwortet GraphQL, bevor gespeichert ist
      return ticket;
    },
  },
});
```

---

## `index.ts`: Start erst nach der Verbindung

Die Verbindung zu MongoDB und der Start von Apollo sind `async`. Deshalb wandert der Aufbau der App in eine Funktion `main()`, die erst dann auf den Port hört, wenn alles bereit ist.

```ts
// backend/src/index.ts
import express from "express";
import { ApolloServer } from "@apollo/server";
import { expressMiddleware } from "@as-integrations/express4";
import { Ticket } from "./models/ticket";
import { TicketRepository } from "./repositories/ticket-repository";
import { TicketService } from "./services/ticket-service";
import { sampleTickets } from "./data/sample-tickets";
import { typeDefs, createResolvers } from "./graphql/schema";

const repository = new TicketRepository();
const service = new TicketService(repository);

async function main() {
  await repository.connect(
    process.env.MONGO_URL ?? "mongodb://localhost:27017/teamboard"
  );

  // Nur beim allerersten Start: leere Datenbank mit Beispieltickets füllen
  if ((await repository.count()) === 0) {
    for (const ticket of sampleTickets) await repository.add(ticket);
    console.log("Seeded sample tickets");
  }

  const app = express();
  app.use(express.json());

  app.get("/tickets", async (req, res) => {
    res.status(200).json(await repository.getAll());
  });

  // ... die übrigen Routen aus Modul 14, jeweils mit async und await
  //     (vollständig in der Lösung, Aufgabe 3)

  const apollo = new ApolloServer({ typeDefs, resolvers: createResolvers(repository) });
  await apollo.start(); // muss fertig sein, bevor die Middleware eingehängt wird
  app.use("/graphql", expressMiddleware(apollo));

  const port = Number(process.env.PORT) || 3000;
  app.listen(port, () =>
    console.log(`TeamBoard backend listening on port ${port} (REST + /graphql)`)
  );
}

main().catch((err) => {
  console.error("Startup failed:", err);
  process.exit(1);
});
```

> **Achtung, ältere Anleitungen:** Viele Beispiele im Netz nutzen `apolloServer.applyMiddleware({ app })`. Das ist die API von Apollo Server 3 und existiert in `@apollo/server` nicht mehr. Richtig ist `app.use("/graphql", expressMiddleware(apollo))`.

---

## Checkpoint

Der GraphQL-Playground unter `http://localhost:3000/graphql` liefert per `tickets`-Query dieselben Daten wie `GET /tickets`; ein Container-Neustart (`docker compose restart backend`) zeigt weiterhin alle zuvor angelegten Tickets und Statuswechsel, weil sie jetzt in MongoDB statt im Arbeitsspeicher liegen.

## Projektbezug

Damit überleben Tickets erstmals einen Server-Neustart. Modul 16 sichert die API mit JWT-Authentifizierung ab.
