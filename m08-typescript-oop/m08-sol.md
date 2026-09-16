# Transfer-Übung Modul 8 - Lösung: End-to-End-Ablauf mit Repository und Service

## Aufgabe 1-3: Repository, Service und Statusübergänge

```ts
// backend/src/index.ts (Ausschnitt)
import { TicketRepository } from "./repositories/ticket-repository";
import { TicketService } from "./services/ticket-service";
import { sampleTickets } from "./data/sample-tickets";

const repository = new TicketRepository();
sampleTickets.forEach((ticket) => repository.add(ticket));

const service = new TicketService(repository);
const ticketId = "t-1";

console.log("Vorher:", repository.findById(ticketId)?.status);
service.moveToNextStatus(ticketId);
console.log("Nach 1. Aufruf:", repository.findById(ticketId)?.status);
service.moveToNextStatus(ticketId);
console.log("Nach 2. Aufruf:", repository.findById(ticketId)?.status);
```

Erwartete Ausgabe:

```text
Vorher: To Do
Nach 1. Aufruf: In Progress
Nach 2. Aufruf: Done
```

## Aufgabe 4: Build, Commit, Push

```bash
npm run build
npm start
git add -A
git commit -m "feat: wire repository and service end-to-end"
git push
```

## Grenzen

Alle Daten leben nur im Arbeitsspeicher - Persistenz (MongoDB) kommt erst in Modul 15 hinzu.
