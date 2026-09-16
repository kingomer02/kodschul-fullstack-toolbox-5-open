# Lab 8.2 - Lösung: Access Modifiers

## Aufgabe 1: `TicketRepository`

```ts
// backend/src/repositories/ticket-repository.ts
import { Ticket } from "../models/ticket";

export class TicketRepository {
  private tickets: Ticket[] = [];

  add(ticket: Ticket): void {
    this.tickets.push(ticket);
  }

  findById(id: string): Ticket | undefined {
    return this.tickets.find((t) => t.id === id);
  }
}
```

## Aufgabe 2: Verwenden

```ts
const repo = new TicketRepository();
repo.add({
  id: "t-1",
  title: "Setup Repo",
  description: "Initial repo structure",
  assignee: "Alex",
  status: "To Do",
});

console.log(repo.findById("t-1")); // Ticket-Objekt
console.log(repo.findById("t-99")); // undefined
```

## Aufgabe 3: Fehlerhafter Direktzugriff

```ts
console.log(repo.tickets);
// Fehler: Property 'tickets' is private and only accessible within class 'TicketRepository'.
```

## Aufgabe 4: Bereinigen

Die fehlerhafte Zeile entfernen - Zugriff erfolgt ausschließlich über `add`/`findById`.

## Grenzen

`TicketRepository` speichert nur im Arbeitsspeicher - eine echte Datenbank (MongoDB) folgt erst in Modul 15.
