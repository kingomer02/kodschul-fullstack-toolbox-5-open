# Lab 16.4 - Lösung: Jeden Eingang schützen, 401 von 403 trennen

## Aufgabe 1: Die Lücke (gemessen 09/2026)

```text
GET  /tickets                  (ohne Token)  -> 401  {"error":"missing token"}
POST /graphql { tickets { title status } }   -> 200  {"data":{"tickets":[{"title":"Setup Repo",...}]}}
POST /graphql mutation { createTicket(title: "Ohne Login angelegt") { id } }
                                             -> 200  {"data":{"createTicket":{"id":"t-1790114268670"}}}
```

Lesen **und** Schreiben ohne Anmeldung.

## Aufgabe 2: Weg A

```ts
app.use("/graphql", requireAuth, expressMiddleware(apollo));
```

```text
GET /graphql (Browser, ohne Token)  -> 401  {"error":"missing token"}
```

Die Apollo-Oberfläche lädt nicht mehr - der Browser schickt beim Öffnen der Seite keinen Token mit.

## Aufgabe 3: Weg B

```ts
// backend/src/auth/require-auth.ts
import { NextFunction, Request, Response } from "express";
import jwt from "jsonwebtoken";

const JWT_SECRET = process.env.JWT_SECRET ?? "dev-only-secret";

// Liefert den Benutzernamen aus einem gültigen Token - oder undefined
export function usernameFromHeader(header: string | undefined): string | undefined {
  if (!header?.startsWith("Bearer ")) return undefined;
  try {
    const payload = jwt.verify(header.slice("Bearer ".length), JWT_SECRET);
    return typeof payload === "object" ? payload.username : undefined;
  } catch {
    return undefined;
  }
}

export function requireAuth(req: Request, res: Response, next: NextFunction) {
  const header = req.headers.authorization;
  if (!header?.startsWith("Bearer ")) {
    return res.status(401).json({ error: "missing token" });
  }
  const username = usernameFromHeader(header);
  if (!username) return res.status(401).json({ error: "invalid token" });
  res.locals.username = username; // für die Routen: WER fragt an?
  next();
}
```

```ts
// backend/src/graphql/schema.ts (Ausschnitte)
import { GraphQLError } from "graphql";

export interface GraphQLContext {
  username?: string; // aus dem Token, undefined ohne gültigen Token
}

// Wirft, wenn kein gültiger Token mitkam - als 401 statt 200
function requireUser(ctx: GraphQLContext): string {
  if (!ctx.username) {
    throw new GraphQLError("not authenticated", {
      extensions: { code: "UNAUTHENTICATED", http: { status: 401 } },
    });
  }
  return ctx.username;
}

// in createResolvers:
tickets: (_: unknown, __: unknown, ctx: GraphQLContext) => {
  requireUser(ctx);
  return repository.getAll();
},
```

```ts
// backend/src/index.ts (Ausschnitt)
const apollo = new ApolloServer<GraphQLContext>({ typeDefs, resolvers: createResolvers(repository, service) });
await apollo.start();
app.use(
  "/graphql",
  expressMiddleware(apollo, {
    // läuft bei JEDER GraphQL-Anfrage: wer fragt an?
    context: async ({ req }) => ({
      username: usernameFromHeader(req.headers.authorization),
    }),
  })
);
```

## Aufgabe 4-5: `createdBy` und 403

```ts
// backend/src/models/ticket.ts
export interface Ticket {
  id: string;
  title: string;
  description: string;
  assignee: string;
  status: "To Do" | "In Progress" | "Done";
  createdBy?: string; // setzt der Server beim Anlegen, nie der Client
}
```

```ts
// backend/src/routes/ticket-routes.ts (Ausschnitte)
const ticket: Ticket = {
  id: `t-${Date.now()}`,
  ...input,
  status: "To Do",
  createdBy: res.locals.username,
};

router.delete("/:id", asyncHandler(async (req, res) => {
  const ticket = await repository.findById(req.params.id);
  if (!ticket) throw ticketNotFound();
  // 401 = wir wissen nicht, wer du bist. 403 = wir wissen es - und du darfst nicht.
  if (ticket.createdBy !== res.locals.username) {
    throw new HttpError(403, "only the creator may delete this ticket");
  }
  await repository.remove(req.params.id);
  res.status(204).end();
}));
```

## Aufgabe 6: Gemessen mit `alex` und `sam` (09/2026)

```text
POST /graphql { tickets { title } }            (ohne Token)  -> 401  {"errors":[{"message":"not authenticated",...,"extensions":{"code":"UNAUTHENTICATED",...}}]}
POST /graphql mutation { createTicket(...) }   (ohne Token)  -> 401  UNAUTHENTICATED
POST /graphql { tickets { title } }            [alex]        -> 200  {"data":{"tickets":[...]}}
POST /tickets {"title":"Von Alex angelegt"}    [alex]        -> 201  {...,"createdBy":"alex"}
POST /tickets {"title":"...","createdBy":"sam"} [alex]       -> 422  Unrecognized key: "createdBy"
DELETE /tickets/<Alex' Ticket>                 [sam]         -> 403  {"error":"only the creator may delete this ticket"}
DELETE /tickets/<Alex' Ticket>                 (ohne Token)  -> 401  {"error":"missing token"}
DELETE /tickets/<Alex' Ticket>                 [alex]        -> 204
DELETE /tickets/t-1                            [alex]        -> 403  (Beispielticket, niemand hat es angelegt)
GET  /graphql  (Browser, ohne Token)                         -> 200  Apollo-Oberfläche lädt
```

**Die Beispieltickets** haben kein `createdBy` - niemand darf sie löschen. Das ist eine Designentscheidung, keine Notwendigkeit: Man könnte ebenso eine Admin-Rolle einführen.

## Commit

```bash
git add -A
git commit -m "feat: GraphQL per Kontext geschützt, createdBy, 403 beim Löschen fremder Tickets"
```

## Grenzen

- Die Fehlerantwort von Apollo enthält im Feld `extensions.stacktrace` den vollständigen Stacktrace - dasselbe Problem wie in Lab 14.5. Apollo lässt ihn weg, wenn `NODE_ENV=production` gesetzt ist.
- Die Nutzer liegen weiterhin im Arbeitsspeicher. Nach einem Neustart des Backends muss man sich neu registrieren, die Tickets samt `createdBy` bleiben aber in MongoDB.
