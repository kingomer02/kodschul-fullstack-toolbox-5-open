# Lab 8.3 - Lösung: Einstieg in Generics

## Aufgabe 1: Generische Basisklasse

```ts
// backend/src/repositories/repository.ts
export class Repository<T extends { id: string }> {
  private items: T[] = [];

  add(item: T): void {
    this.items.push(item);
  }

  findById(id: string): T | undefined {
    return this.items.find((item) => item.id === id);
  }
}
```

## Aufgabe 2: `TicketRepository` darauf umstellen

```ts
// backend/src/repositories/ticket-repository.ts
import { Ticket } from "../models/ticket";
import { Repository } from "./repository";

export class TicketRepository extends Repository<Ticket> {}
```

## Aufgabe 3: Bestehendes Verhalten prüfen

```ts
const repo = new TicketRepository();
repo.add({
  id: "t-1",
  title: "Setup Repo",
  description: "Initial repo structure",
  assignee: "Alex",
  status: "To Do",
});

console.log(repo.findById("t-1")); // unverändert wie in Lab 8.2
```

## Aufgabe 4: Zweiter generischer Anwendungsfall

```ts
const labelRepo = new Repository<{ id: string; label: string }>();
labelRepo.add({ id: "l-1", label: "urgent" });
console.log(labelRepo.findById("l-1")); // { id: "l-1", label: "urgent" }
```

## Grenzen

`Repository<T>` speichert weiterhin nur im Arbeitsspeicher - Persistenz (MongoDB) kommt in Modul 15 als eigener Baustein hinzu, ohne dass sich dieses Interface grundlegend ändert.

## Aufgabe 5-6: `TicketService`

```ts
// backend/src/services/ticket-service.ts
import { Ticket } from "../models/ticket";
import { TicketRepository } from "../repositories/ticket-repository";

export class TicketService {
  constructor(private repository: TicketRepository) {}

  moveToNextStatus(id: string): Ticket | undefined {
    const ticket = this.repository.findById(id);
    if (!ticket) return undefined;

    const order: Ticket["status"][] = ["To Do", "In Progress", "Done"];
    const nextIndex = Math.min(
      order.indexOf(ticket.status) + 1,
      order.length - 1
    );
    ticket.status = order[nextIndex];
    return ticket;
  }
}
```

```ts
const repo = new TicketRepository();
repo.add({
  id: "t-1",
  title: "Setup Repo",
  description: "Initial repo structure",
  assignee: "Alex",
  status: "To Do",
});

const service = new TicketService(repo);
service.moveToNextStatus("t-1"); // status wird "In Progress"
service.moveToNextStatus("t-1"); // status wird "Done"
```

`repository` ist `private`, weil `TicketService` es nur intern braucht - Außencode ruft ausschließlich `moveToNextStatus` auf, nicht `repository.findById` direkt.
