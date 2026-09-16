# Modul 18: Einstieg in React

## Lab 18.2 - Komponenten und State: Ticket-Karten

---

## Lab-Ziel

Du kannst eine `TicketCard`-Komponente mit Props bauen und mehrere davon aus einem lokalen State-Array in einer `Column`-Komponente rendern.

**Leitfragen:**

<details>
<summary>Was ist der Unterschied zwischen Props und State in React?</summary>

Props werden einer Komponente von außen übergeben und sind aus ihrer eigenen Sicht unveränderlich; State wird innerhalb einer Komponente verwaltet und kann sich durch Nutzerinteraktion ändern.

</details>

<details>
<summary>Warum bekommt jedes Element in `tickets.map(...)` einen `key`?</summary>

React nutzt `key`, um einzelne Listenelemente bei Änderungen eindeutig wiederzuerkennen, statt bei jeder Änderung die komplette Liste neu zu erzeugen.

</details>

---

## `TicketCard`-Komponente mit Props

```tsx
// frontend/src/components/TicketCard.tsx
interface TicketCardProps {
  title: string;
  assignee: string;
}

export function TicketCard({ title, assignee }: TicketCardProps) {
  return (
    <div className="card mb-2">
      <div className="card-body">
        <p className="mb-1">{title}</p>
        <small className="text-muted">{assignee || "Nicht zugewiesen"}</small>
      </div>
    </div>
  );
}
```

## `Column`-Komponente mit lokalem State

```tsx
// frontend/src/components/Column.tsx
import { useState } from "react";
import { TicketCard } from "./TicketCard";

interface Ticket {
  id: string;
  title: string;
  assignee: string;
}

interface ColumnProps {
  title: string;
  initialTickets: Ticket[];
}

export function Column({ title, initialTickets }: ColumnProps) {
  const [tickets] = useState<Ticket[]>(initialTickets);

  return (
    <div className="column">
      <h2>{title}</h2>
      {tickets.map((ticket) => (
        <TicketCard
          key={ticket.id}
          title={ticket.title}
          assignee={ticket.assignee}
        />
      ))}
    </div>
  );
}
```

---

## Checkpoint

`<Column title="To Do" initialTickets={[...]} />` rendert eine Überschrift und für jedes Ticket im Array genau eine `TicketCard` mit dem jeweiligen Titel und der jeweiligen `assignee`.

## Projektbezug

Weiter geht es mit Lab 18.3: das vollständige React-Projekt-Setup mit allen drei Spalten und Bootstrap/Sass aus Modul 17.
