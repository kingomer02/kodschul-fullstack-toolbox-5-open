# Transfer-Übung Modul 14 - Lösung: Vollständigen Ticket-Lebenszyklus über die API abbilden

## Aufgabe 1: Ticket anlegen

```bash
curl -X POST http://localhost:3000/tickets \
  -H "Content-Type: application/json" \
  -d '{"title": "Neues Feature", "description": "Testen", "assignee": "Alex"}'
# 201 { "id": "t-1700000000000", "status": "To Do", "assignee": "Alex", ... }
```

## Aufgabe 2: Zuweisen

```bash
curl -X PATCH http://localhost:3000/tickets/t-1700000000000/assign \
  -H "Content-Type: application/json" -d '{"assignee": "Sam"}'
# { ..., "assignee": "Sam" }
```

## Aufgabe 3-4: Status zweimal weiterbewegen und prüfen

```bash
curl -X PATCH http://localhost:3000/tickets/t-1700000000000/status
# status: "In Progress"
curl -X PATCH http://localhost:3000/tickets/t-1700000000000/status
# status: "Done"
curl http://localhost:3000/tickets/t-1700000000000
# { "status": "Done", "assignee": "Sam", ... }
```

## Aufgabe 5: Fehlerfall

```bash
curl -X PATCH http://localhost:3000/tickets/unbekannte-id/assign \
  -H "Content-Type: application/json" -d '{"assignee": "Sam"}'
# 404 { "error": "ticket not found" }
```

## Grenzen

Ein Neustart des Containers setzt dieses neu angelegte Ticket zurück auf den `sample-tickets.ts`-Stand, da noch keine Persistenz existiert (folgt in Modul 15).
