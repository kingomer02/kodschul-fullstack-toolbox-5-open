# Lab 14.4 - Lösung: Ressourcen schneiden und HTTP-Methoden richtig einsetzen

## Aufgabe 1: Entscheidung

- Ändern dürfen: `title`, `description`, `assignee` - reine Daten ohne Regel.
- **Nicht** ändern darf: `status`. Dafür gibt es eine Fachregel (ein Schritt vorwärts), die in `TicketService.moveToNextStatus` steckt. Ein freies Update würde sie umgehen.
- `id` sowieso nicht: Sie steht in der URL und identifiziert die Ressource.

## Aufgabe 2: `Repository<T>`

```ts
// backend/src/repositories/repository.ts (Ergänzung)
update(id: string, changes: Partial<Omit<T, "id">>): T | undefined {
  const item = this.findById(id);
  if (!item) return undefined;
  Object.assign(item, changes);
  return item;
}

remove(id: string): boolean {
  const index = this.items.findIndex((item) => item.id === id);
  if (index === -1) return false;
  this.items.splice(index, 1);
  return true;
}
```

`Partial<Omit<T, "id">>`: alle Felder optional, aber `id` gar nicht erst erlaubt. So verhindert schon der Compiler, dass jemand die ID ändert.

## Aufgabe 3-5: Routen

```ts
// backend/src/index.ts (Ergänzung)
app.post("/tickets", (req, res) => {
  // ... wie bisher ...
  repository.add(ticket);
  res.status(201).location(`/tickets/${ticket.id}`).json(ticket);
});

app.patch("/tickets/:id", (req, res) => {
  const { title, description, assignee, status } = req.body;
  if (status !== undefined) {
    return res
      .status(400)
      .json({ error: "status is changed via PATCH /tickets/:id/status" });
  }
  const changes: Partial<Omit<Ticket, "id">> = {};
  if (title !== undefined) changes.title = title;
  if (description !== undefined) changes.description = description;
  if (assignee !== undefined) changes.assignee = assignee;
  const ticket = repository.update(req.params.id, changes);
  if (!ticket) return res.status(404).json({ error: "ticket not found" });
  res.status(200).json(ticket);
});

app.delete("/tickets/:id", (req, res) => {
  const removed = repository.remove(req.params.id);
  if (!removed) return res.status(404).json({ error: "ticket not found" });
  res.status(204).end();
});
```

Die `if (… !== undefined)`-Zeilen sind nötig: Würde man `{ title, description, assignee }` direkt übergeben, landeten fehlende Felder als `undefined` im Ticket. Lab 14.6 ersetzt das durch ein Schema.

## Aufgabe 6: Gemessene Antworten (09/2026)

```text
POST   /tickets {"title":"Doku schreiben"}      -> 201  Location: /tickets/t-1790113406435
PATCH  /tickets/t-1 {"assignee":"Ömer",...}     -> 200  {...,"title":"Setup Repo (neu)","assignee":"Ömer","status":"To Do"}
PATCH  /tickets/t-1 {"status":"Done"}           -> 400  {"error":"status is changed via PATCH /tickets/:id/status"}
PATCH  /tickets/gibts-nicht {"title":"x"}       -> 404  {"error":"ticket not found"}
DELETE /tickets/t-2                              -> 204  (kein Body)
DELETE /tickets/t-2                              -> 404  {"error":"ticket not found"}
PUT    /tickets/t-1                              -> 404  <!DOCTYPE html> ... <pre>Cannot PUT /tickets/t-1</pre>
```

Die letzte Zeile ist der Einstieg in Lab 14.5: Für unbekannte Routen antwortet Express mit einer **HTML-Seite**, nicht mit JSON.

## Commit

```bash
git add -A
git commit -m "feat: PATCH /tickets/:id, DELETE /tickets/:id, Location-Header bei POST"
```

## Grenzen

`PUT` wird bewusst nicht gebaut: Ein Ticket komplett zu ersetzen hätte dasselbe Status-Problem wie ein freies `PATCH`. Streng genommen wäre auf `PUT /tickets/t-1` die Antwort `405 Method Not Allowed` richtiger als `404` - Express unterscheidet das von sich aus nicht.
