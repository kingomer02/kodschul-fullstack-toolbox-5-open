# Lab 7.3 - Lösung: Datenmodelle typisieren

## Aufgabe 1: `Ticket`-Interface

```ts
// backend/src/models/ticket.ts
export interface Ticket {
  id: string;
  title: string;
  description: string;
  assignee: string;
  status: "To Do" | "In Progress" | "Done";
}
```

## Aufgabe 2: Beispielobjekte

```ts
const ticket1: Ticket = {
  id: "t-1",
  title: "Setup Repo",
  description: "Initial repo structure and README",
  assignee: "Alex",
  status: "To Do",
};

const ticket2: Ticket = {
  id: "t-2",
  title: "Add CI pipeline",
  description: "Lint and build on every push",
  assignee: "Sam",
  status: "In Progress",
};
```

## Aufgabe 3-4: Fehler beobachten und korrigieren

```ts
const invalidTicket: Ticket = { ...ticket1, status: "Todo" };
// Fehler: Type '"Todo"' is not assignable to type '"To Do" | "In Progress" | "Done"'.
```

Korrektur: `status: "To Do"` (exakte Schreibweise gemäß Contract).

## Grenzen

Dieses Modell beschreibt nur die Datenform - Logik zum Erstellen/Ändern von Tickets folgt in Modul 8 (`TicketService`/`TicketRepository`).
