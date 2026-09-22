# Lab 14.6 - Lösung: Eingaben validieren mit zod

## Aufgabe 1: Ist-Zustand

Ohne Validierung speichert die API, was kommt (gemessen 09/2026):

```text
POST /tickets {"title":42,"priority":"hoch"} -> 201  {"id":"t-...","title":42,"description":"","assignee":"","status":"To Do"}
POST /tickets {"title":"   "}                -> 201  {"id":"t-...","title":"   ","description":"","assignee":"","status":"To Do"}
```

Der Titel ist eine **Zahl**, obwohl das `Ticket`-Interface `string` verlangt - TypeScript hat davon nichts mitbekommen. Das Feld `priority` wird still verworfen, der Client merkt nicht, dass es nie gespeichert wurde.

## Aufgabe 2: Installation

```bash
cd backend
npm install zod
```

Gemessen 09/2026: `zod@4.6.5`. zod bringt seine Typen selbst mit, es braucht kein `@types/zod`.

## Aufgabe 3-4: Schemas und `validate`

```ts
// backend/src/validation/ticket-schemas.ts
import { z } from "zod";
import { HttpError } from "../http/http-error";

// Felder einmal definieren, dann für Anlegen und Ändern kombinieren
const title = z.string().trim().min(1).max(100);
const description = z.string().max(2000);
const assignee = z.string().trim().max(50);

export const createTicketSchema = z.strictObject({
  title,
  description: description.default(""),
  assignee: assignee.default(""),
});

// Bewusst OHNE .default(): .partial() würde die Defaults übernehmen und
// bei jedem PATCH description/assignee auf "" zurücksetzen
export const updateTicketSchema = z
  .strictObject({ title, description, assignee })
  .partial()
  .refine((body) => Object.keys(body).length > 0, {
    message: "at least one field is required",
  });

export const assignSchema = z.strictObject({ assignee: assignee.min(1) });

export type CreateTicketInput = z.infer<typeof createTicketSchema>;
export type UpdateTicketInput = z.infer<typeof updateTicketSchema>;

// Prüft und liefert typisierte Daten - oder wirft 422 mit Details
export function validate<S extends z.ZodType>(schema: S, data: unknown): z.infer<S> {
  const result = schema.safeParse(data);
  if (!result.success) {
    const details = result.error.issues.map((issue) => ({
      field: issue.path.join(".") || "(root)",
      message: issue.message,
    }));
    throw new HttpError(422, "validation failed", details);
  }
  return result.data;
}
```

**Warum `status` nicht im Update-Schema steht:** `z.strictObject` lehnt jedes Feld ab, das nicht definiert ist. Die Regel aus Lab 14.4 ("Status nur über die eigene Aktion") erzwingt jetzt das Schema, nicht mehr eine Handprüfung.

## Aufgabe 5: Routen

```ts
// backend/src/routes/ticket-routes.ts (Ausschnitte)
router.post("/", (req, res) => {
  const input = validate(createTicketSchema, req.body);
  const ticket: Ticket = { id: `t-${Date.now()}`, ...input, status: "To Do" };
  repository.add(ticket);
  res.status(201).location(`/tickets/${ticket.id}`).json(ticket);
});

router.patch("/:id", (req, res) => {
  const changes = validate(updateTicketSchema, req.body);
  const ticket = repository.update(req.params.id, changes);
  if (!ticket) throw ticketNotFound();
  res.status(200).json(ticket);
});

router.patch("/:id/assign", (req, res) => {
  const { assignee } = validate(assignSchema, req.body);
  const ticket = service.assign(req.params.id, assignee);
  if (!ticket) throw ticketNotFound();
  res.status(200).json(ticket);
});
```

Die Fehler-Middleware aus Lab 14.5 bleibt unverändert: `validate` wirft einen `HttpError`, den sie schon kennt.

## Aufgabe 6: Gemessene Antworten (09/2026)

```text
POST  /tickets {"title":"  Tests schreiben  ","assignee":"Sam"}
      -> 201  {"id":"t-...","title":"Tests schreiben","description":"","assignee":"Sam","status":"To Do"}
POST  /tickets {}
      -> 422  {"error":"validation failed","details":[{"field":"title","message":"Invalid input: expected string, received undefined"}]}
POST  /tickets {"title":42,"priority":"hoch"}
      -> 422  {"error":"validation failed","details":[
                {"field":"title","message":"Invalid input: expected string, received number"},
                {"field":"(root)","message":"Unrecognized key: \"priority\""}]}
POST  /tickets {"title":"   "}
      -> 422  {"error":"validation failed","details":[{"field":"title","message":"Too small: expected string to have >=1 characters"}]}
PATCH /tickets/t-1 {"status":"Done"}
      -> 422  {"error":"validation failed","details":[
                {"field":"(root)","message":"Unrecognized key: \"status\""},
                {"field":"(root)","message":"at least one field is required"}]}
PATCH /tickets/t-1 {}
      -> 422  {"error":"validation failed","details":[{"field":"(root)","message":"at least one field is required"}]}
PATCH /tickets/t-1/assign {"assignee":""}
      -> 422  {"error":"validation failed","details":[{"field":"assignee","message":"Too small: expected string to have >=1 characters"}]}
```

## Aufgabe 7: Die Stolperfalle, gemessen

Mit `updateTicketSchema = createTicketSchema.partial()`:

```text
PATCH /tickets/t-1 {"assignee":"Ömer"}
  -> 200  {"id":"t-1","title":"Setup Repo","description":"","assignee":"Ömer","status":"To Do"}
```

Die Beschreibung `"Initial repo structure and README"` ist **weg** - ohne Fehlermeldung. Mit dem getrennten Update-Schema oben bleibt sie erhalten:

```text
PATCH /tickets/t-1 {"assignee":"Ömer"}
  -> 200  {"id":"t-1","title":"Setup Repo","description":"Initial repo structure and README","assignee":"Ömer","status":"To Do"}
```

## Commit

```bash
git add -A
git commit -m "feat: Eingaben mit zod validieren, 422 mit Details"
```

## Grenzen

Die Meldungen sind die englischen Standardtexte von zod. Für eine Oberfläche würde man sie übersetzen oder eigene Texte im Schema hinterlegen (`z.string().min(1, "Titel darf nicht leer sein")`).
