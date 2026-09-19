# Modul 15: GraphQL und MongoDB

## Lab 15.3 - MongoDB-Integration für TeamBoard

---

## Lab-Ziel

Du bindest den offiziellen MongoDB-Treiber ins Backend ein, ersetzt die In-Memory-Speicherung durch eine echte MongoDB-Collection und ergänzt ein GraphQL-Schema für Tickets neben der bestehenden REST-API.

**Leitfragen:**

<details>
<summary>Warum reicht es, nur `TicketRepository` auf MongoDB umzustellen, statt auch `TicketService` oder die Express-Routen zu ändern?</summary>

`TicketRepository` kapselt die Datenhaltung; `TicketService` und die Routen rufen weiterhin dieselben Methodennamen (`add`, `findById`, `getAll`) auf und müssen nicht wissen, ob die Daten im Speicher oder in MongoDB liegen.

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

export class TicketRepository {
  private collection: Collection<Ticket> | undefined;

  async connect(mongoUrl: string): Promise<void> {
    const client = new MongoClient(mongoUrl);
    await client.connect();
    this.collection = client.db().collection<Ticket>("tickets");
  }

  async add(ticket: Ticket): Promise<void> {
    await this.collection!.insertOne(ticket);
  }

  async findById(id: string): Promise<Ticket | null> {
    return this.collection!.findOne({ id });
  }

  async getAll(): Promise<Ticket[]> {
    return this.collection!.find().toArray();
  }
}
```

- Alle Methoden werden `async`, weil Datenbankzugriffe nie synchron ablaufen - die Express-Routen aus Modul 14 brauchen dafür `await` vor jedem Aufruf.

---

## GraphQL-Schema für Tickets

```ts
// backend/src/graphql/schema.ts
import gql from "graphql-tag";
import { TicketRepository } from "../repositories/ticket-repository";

export const typeDefs = gql`
  type Ticket {
    id: ID!
    title: String!
    description: String
    assignee: String
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
    createTicket: (
      _: unknown,
      args: { title: string; description?: string; assignee?: string }
    ) => {
      const ticket = {
        id: `t-${Date.now()}`,
        title: args.title,
        description: args.description ?? "",
        assignee: args.assignee ?? "",
        status: "To Do" as const,
      };
      repository.add(ticket);
      return ticket;
    },
  },
});
```

```ts
// backend/src/index.ts (Ergänzung)
import { ApolloServer } from "@apollo/server";
import { expressMiddleware } from "@as-integrations/express4";
import { typeDefs, createResolvers } from "./graphql/schema";

async function start() {
  await repository.connect(
    process.env.MONGO_URL ?? "mongodb://mongo:27017/teamboard"
  );

  const apolloServer = new ApolloServer({
    typeDefs,
    resolvers: createResolvers(repository),
  });
  await apolloServer.start();
  apolloServer.applyMiddleware({ app, path: "/graphql" });

  app.listen(port, () =>
    console.log(`TeamBoard backend listening on port ${port}`)
  );
}

start();
```

---

## Checkpoint

Der GraphQL-Playground unter `http://localhost:3000/graphql` liefert per `tickets`-Query dieselben Daten wie `GET /tickets`; ein Container-Neustart (`docker compose restart backend`) zeigt weiterhin alle zuvor angelegten Tickets, weil sie jetzt in MongoDB statt im Arbeitsspeicher liegen.

## Projektbezug

Damit überleben Tickets erstmals einen Server-Neustart. Modul 16 sichert die API mit JWT-Authentifizierung ab.
