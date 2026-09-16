# Lab 14.2 - Lösung: Express-REST-API für TeamBoard

## Aufgabe 1: Installation

```bash
cd backend
npm install express
npm install --save-dev @types/express
```

## Aufgabe 2: `getAll()`

```ts
// backend/src/repositories/repository.ts (Ergänzung)
getAll(): T[] {
  return this.items;
}
```

## Aufgabe 3: `assign()`

```ts
// backend/src/services/ticket-service.ts (Ergänzung)
assign(id: string, assignee: string): Ticket | undefined {
  const ticket = this.repository.findById(id);
  if (!ticket) return undefined;
  ticket.assignee = assignee;
  return ticket;
}
```

## Aufgabe 4: Express-Server

Siehe vollständiges `backend/src/index.ts` im Theorieteil (Lab 14.2, Abschnitt "Express-Server mit Ticket-Routen").

## Aufgabe 5: Testen

```bash
npm run build && npm start
# TeamBoard backend listening on port 3000

curl http://localhost:3000/tickets
# [{ "id": "t-1", ... }, ...]

curl -X PATCH http://localhost:3000/tickets/t-1/status
# { "id": "t-1", "status": "In Progress", ... }

curl http://localhost:3000/tickets/unbekannte-id
# 404 { "error": "ticket not found" }
```

## Aufgabe 6: Commit

```bash
git add -A
git commit -m "feat: add Express REST API for tickets"
```

## Grenzen

Daten leben weiterhin nur im Arbeitsspeicher - ein Server-Neustart setzt den Ticket-Stand auf `sample-tickets.ts` zurück. Persistenz folgt in Modul 15 mit MongoDB.
