# Lab 14.5 - Lösung: Router und zentrale Fehlerbehandlung

## Aufgabe 1: Ist-Zustand (gemessen 09/2026)

```text
POST /tickets '{"title": "kaputt",}'  -> 400
<!DOCTYPE html> ... <pre>SyntaxError: Expected double-quoted property name in JSON at position 19
  at JSON.parse (<anonymous>)
  at parse (/.../backend/node_modules/body-parser/lib/types/json.js:96:19) ...

GET /gibts/nicht                      -> 404
<!DOCTYPE html> ... <pre>Cannot GET /gibts/nicht</pre>
```

Der Client bekommt den kompletten Stacktrace mit Dateipfaden. Im Container stünde dort `/app/node_modules/...`.

## Aufgabe 2: Fehlerklasse

```ts
// backend/src/http/http-error.ts
export class HttpError extends Error {
  constructor(
    public readonly status: number,
    message: string,
    public readonly details?: unknown
  ) {
    super(message);
  }
}

export const ticketNotFound = () => new HttpError(404, "ticket not found");
```

## Aufgabe 3: Middleware

```ts
// backend/src/http/error-handler.ts
import { ErrorRequestHandler, RequestHandler } from "express";
import { HttpError } from "./http-error";

// Greift, wenn keine Route passt - ersetzt Express' HTML-Seite "Cannot GET ..."
export const notFoundHandler: RequestHandler = (req, res) => {
  res.status(404).json({ error: `route not found: ${req.method} ${req.path}` });
};

// Vier Parameter: daran erkennt Express eine Fehler-Middleware
export const errorHandler: ErrorRequestHandler = (err, req, res, _next) => {
  if (err instanceof HttpError) {
    res.status(err.status).json({ error: err.message, details: err.details });
    return;
  }
  if (err.type === "entity.parse.failed") {
    res.status(400).json({ error: "invalid JSON body" });
    return;
  }
  console.error(err);
  res.status(500).json({ error: "internal server error" });
};
```

## Aufgabe 4: Router

```ts
// backend/src/routes/ticket-routes.ts (Ausschnitt)
import { Router } from "express";
import { Ticket } from "../models/ticket";
import { TicketRepository } from "../repositories/ticket-repository";
import { TicketService } from "../services/ticket-service";
import { HttpError, ticketNotFound } from "../http/http-error";

export function ticketRoutes(repository: TicketRepository, service: TicketService): Router {
  const router = Router();

  router.get("/:id", (req, res) => {
    const ticket = repository.findById(req.params.id);
    if (!ticket) throw ticketNotFound();
    res.status(200).json(ticket);
  });

  router.delete("/:id", (req, res) => {
    if (!repository.remove(req.params.id)) throw ticketNotFound();
    res.status(204).end();
  });

  // ... die übrigen Routen nach demselben Muster
  return router;
}
```

Die Funktion bekommt Repository und Service hineingereicht, statt sie selbst zu erzeugen - dasselbe Prinzip wie beim `TicketService` in Modul 8.

## Aufgabe 5: `index.ts`

```ts
// backend/src/index.ts
import express from "express";
import { TicketRepository } from "./repositories/ticket-repository";
import { TicketService } from "./services/ticket-service";
import { sampleTickets } from "./data/sample-tickets";
import { ticketRoutes } from "./routes/ticket-routes";
import { errorHandler, notFoundHandler } from "./http/error-handler";

const repository = new TicketRepository();
sampleTickets.forEach((ticket) => repository.add(ticket));
const service = new TicketService(repository);

const app = express();
app.use(express.json());

app.use("/tickets", ticketRoutes(repository, service));

app.use(notFoundHandler); // nach allen Routen
app.use(errorHandler); // ganz am Ende

const port = Number(process.env.PORT) || 3000;
app.listen(port, () =>
  console.log(`TeamBoard backend listening on port ${port}`)
);
```

**Reihenfolge:** Express geht die Middleware von oben nach unten durch. Stünde `notFoundHandler` vor den Routen, bekäme **jede** Anfrage `404`. Die Fehler-Middleware wird nur bei Fehlern angesprungen - aber nur, wenn sie **nach** der Stelle registriert ist, an der der Fehler entsteht.

## Aufgabe 6: Gemessene Antworten danach (09/2026)

```text
POST /tickets '{"title": "kaputt",}'  -> 400  {"error":"invalid JSON body"}
GET  /gibts/nicht                     -> 404  {"error":"route not found: GET /gibts/nicht"}
PUT  /tickets/t-1                     -> 404  {"error":"route not found: PUT /tickets/t-1"}
GET  /tickets/gibts-nicht             -> 404  {"error":"ticket not found"}
POST /tickets '{}'                    -> 400  {"error":"title is required"}
GET  /tickets/boom  (wirft new Error) -> 500  {"error":"internal server error"}
```

Server-Log beim `500`:

```text
Error: Datenbank weg
    at .../dist/routes/ticket-routes.js:8:39
    at Layer.handle [as handle_request] (.../node_modules/express/lib/router/layer.js:95:5)
    ...
```

Der Client erfährt nichts über Interna, die Entwicklerin sieht im Log alles.

## Commit

```bash
git add -A
git commit -m "refactor: Ticket-Routen als Router, zentrale Fehlerbehandlung"
```

## Grenzen

**Wichtig für Modul 15:** Express 4 fängt nur Fehler aus **synchronen** Routen. Wirft eine `async`-Route, erreicht der Fehler die Fehler-Middleware nicht - der ganze Server stürzt ab. Sobald die Routen in Lab 15.3 `async` werden, braucht es deshalb einen kleinen Wrapper. Das kommt in Lab 15.4.
