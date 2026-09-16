# Transfer-Übung Modul 7 - Lösung: Typisierte Beispieldaten mit Auswertung

## Aufgabe 1-2: Beispieldaten und Auswertungsfunktion

```ts
// backend/src/data/sample-tickets.ts
import { Ticket } from "../models/ticket";

export const sampleTickets: Ticket[] = [
  { id: "t-1", title: "Setup Repo", description: "Initial structure", assignee: "Alex", status: "To Do" },
  { id: "t-2", title: "Add CI pipeline", description: "Lint and build", assignee: "Sam", status: "In Progress" },
  { id: "t-3", title: "Write README", description: "Project overview", assignee: "Alex", status: "Done" },
];

export function countByStatus(tickets: Ticket[]): Record<Ticket["status"], number> {
  const counts: Record<Ticket["status"], number> = { "To Do": 0, "In Progress": 0, "Done": 0 };
  for (const ticket of tickets) {
    counts[ticket.status]++;
  }
  return counts;
}
```

## Aufgabe 3-4: Aufruf und Build

```ts
// backend/src/index.ts (Ausschnitt)
import { sampleTickets, countByStatus } from "./data/sample-tickets";

console.log(countByStatus(sampleTickets));
```

```bash
npm run build
npm start
# { 'To Do': 1, 'In Progress': 1, 'Done': 1 }
```

## Grenzen

`countByStatus` liest nur - Schreiboperationen (Status ändern) übernimmt erst `TicketService` in Modul 8.
