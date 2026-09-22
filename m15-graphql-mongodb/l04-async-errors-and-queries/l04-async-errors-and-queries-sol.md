# Lab 15.4 - Lösung: async-Fehler abfangen und Abfragen in die Datenbank verlegen

## Aufgabe 1: Der Absturz (gemessen 09/2026)

```text
GET /tickets/gibts-nicht  -> Verbindung bricht ab (UND_ERR_SOCKET)
GET /tickets              -> Connection refused - der Server läuft nicht mehr
```

Server-Log:

```text
Connected to MongoDB
Seeded sample tickets
TeamBoard backend listening on port 3000 (REST + /graphql)
.../dist/http/http-error.js:14
const ticketNotFound = () => new HttpError(404, "ticket not found");
                             ^

HttpError: ticket not found
  status: 404,
  details: undefined
}

Node.js v24.21.0
```

Ein einziges falsches Ticket beendet den Prozess für alle. Im Container ist `backend` danach `Exited (1)`.

## Aufgabe 2: Warum

Die Routen sind seit Lab 15.3 `async`. Ein `throw` in einer `async`-Funktion wird zu einer abgelehnten Promise. Express 4 ignoriert den Rückgabewert von Handlern - die Ablehnung erreicht nie `next()` und damit nie die Fehler-Middleware. Node beendet den Prozess bei unbehandelten Ablehnungen.

## Aufgabe 3: Wrapper

```ts
// backend/src/http/async-handler.ts
import { NextFunction, Request, RequestHandler, Response } from "express";

type Params = Record<string, string>; // Pfadparameter wie :id sind immer Text

export function asyncHandler(
  handler: (req: Request<Params>, res: Response, next: NextFunction) => Promise<unknown>
): RequestHandler<Params> {
  return (req, res, next) => {
    handler(req, res, next).catch(next);
  };
}
```

```ts
// backend/src/routes/ticket-routes.ts (Ausschnitt)
router.get("/:id", asyncHandler(async (req, res) => {
  const ticket = await repository.findById(req.params.id);
  if (!ticket) throw ticketNotFound();
  res.status(200).json(ticket);
}));
```

## Aufgabe 4-6: Repository

```ts
// backend/src/repositories/ticket-repository.ts (Ausschnitte)
import { Collection, Filter, MongoClient } from "mongodb";

async connect(url: string): Promise<void> {
  const client = new MongoClient(url);
  await client.connect();
  this.collection = client.db().collection<Ticket>("tickets");
  // Unsere id ist der fachliche Schlüssel - MongoDB soll Duplikate verhindern
  await this.collection.createIndex({ id: 1 }, { unique: true });
  console.log("Connected to MongoDB");
}

// Filtern, Sortieren und Blättern erledigt jetzt die Datenbank
async find(query: TicketQuery): Promise<Page<Ticket>> {
  const filter: Filter<Ticket> = {};
  if (query.status) filter.status = query.status;
  if (query.assignee) filter.assignee = query.assignee;

  let cursor = this.collection.find(filter, withoutId);
  if (query.sort) {
    cursor = cursor
      .sort({ [query.sort]: query.order === "desc" ? -1 : 1 })
      .collation({ locale: "de" }); // sonst: Großbuchstaben vor Kleinbuchstaben
  }
  if (query.offset) cursor = cursor.skip(query.offset);
  if (query.limit) cursor = cursor.limit(query.limit);

  // Beide Abfragen laufen parallel - total zählt ohne skip/limit
  const [items, total] = await Promise.all([
    cursor.toArray(),
    this.collection.countDocuments(filter),
  ]);
  return { items, total };
}
```

Das `update` des Repositorys aus 15.3 wird in der Vertiefung zu `findOneAndUpdate` mit `returnDocument: "after"` - so liefert ein einziger Datenbankaufruf das geänderte Ticket zurück.

## Gemessene Antworten danach (09/2026)

```text
GET  /tickets/gibts-nicht      -> 404  {"error":"ticket not found"}
POST /tickets {"title":""}     -> 422  {"error":"validation failed","details":[{"field":"title","message":"Too small: ..."}]}
GET  /tickets?status=To%20Do&sort=title&limit=2&offset=1
                               -> 200  X-Total-Count: 3  [backup einrichten | Setup Repo]
DELETE /tickets/t-2            -> 204
DELETE /tickets/t-2            -> 404
```

**Aufgabe 5, gemessen** mit vier Tickets:

```text
ohne collation:  API dokumentieren | Containerize backend | Setup Repo | backup einrichten
mit collation:   API dokumentieren | backup einrichten | Containerize backend | Setup Repo
```

## Commit

```bash
git add -A
git commit -m "fix: async-Fehler an die Fehler-Middleware, Filter/Sortierung/Paginierung in MongoDB"
```

## Grenzen

Der Index auf `id` wird bei jedem Start angelegt - existiert er schon, macht MongoDB nichts. Für Filter auf `status` lohnt sich ein weiterer Index erst bei vielen Tickets; bei drei Dokumenten liest MongoDB ohnehin alles.
