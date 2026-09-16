# Modul 14: REST-APIs mit Express

## Lab 14.2 - Express-REST-API für TeamBoard

---

## Lab-Ziel

Du verwandelst `index.ts` von einem einmalig durchlaufenden Skript in einen dauerhaft laufenden Express-Server mit echten Ticket-Endpunkten, aufbauend auf `TicketRepository`/`TicketService` aus Modul 8.

**Leitfragen:**

<details>
<summary>Warum reichen `TicketRepository` und `TicketService` aus Modul 8 fast unverändert für die REST-API?</summary>

Sie kapseln bereits die Datenhaltung und die Statuslogik - die Routen rufen diese Methoden nur noch über HTTP auf, statt sie direkt in `index.ts` aufzurufen.

</details>

<details>
<summary>Warum bekommt `TicketService` jetzt eine `assign`-Methode?</summary>

Zuweisen einer Person war bisher nur ein Feld im `Ticket`-Interface (Modul 7), aber keine eigene Aktion - die REST-API braucht dafür einen expliziten Endpunkt und damit eine passende Service-Methode.

</details>

---

## Repository und Service erweitern

```ts
// backend/src/repositories/repository.ts (Ergänzung)
export class Repository<T extends { id: string }> {
  private items: T[] = [];

  add(item: T): void {
    this.items.push(item);
  }

  findById(id: string): T | undefined {
    return this.items.find((item) => item.id === id);
  }

  getAll(): T[] {
    return this.items;
  }
}
```

```ts
// backend/src/services/ticket-service.ts (Ergänzung)
assign(id: string, assignee: string): Ticket | undefined {
  const ticket = this.repository.findById(id);
  if (!ticket) return undefined;
  ticket.assignee = assignee;
  return ticket;
}
```

---

## Express-Server mit Ticket-Routen

```ts
// backend/src/index.ts
import express from "express";
import { TicketRepository } from "./repositories/ticket-repository";
import { TicketService } from "./services/ticket-service";
import { sampleTickets } from "./data/sample-tickets";

const repository = new TicketRepository();
sampleTickets.forEach((ticket) => repository.add(ticket));
const service = new TicketService(repository);

const app = express();
app.use(express.json());

app.get("/tickets", (req, res) => {
  res.status(200).json(repository.getAll());
});

app.get("/tickets/:id", (req, res) => {
  const ticket = repository.findById(req.params.id);
  if (!ticket) return res.status(404).json({ error: "ticket not found" });
  res.status(200).json(ticket);
});

app.post("/tickets", (req, res) => {
  const { title, description, assignee } = req.body;
  if (!title) return res.status(400).json({ error: "title is required" });
  const ticket = {
    id: `t-${Date.now()}`,
    title,
    description: description ?? "",
    assignee: assignee ?? "",
    status: "To Do" as const,
  };
  repository.add(ticket);
  res.status(201).json(ticket);
});

app.patch("/tickets/:id/assign", (req, res) => {
  const { assignee } = req.body;
  if (!assignee) return res.status(400).json({ error: "assignee is required" });
  const ticket = service.assign(req.params.id, assignee);
  if (!ticket) return res.status(404).json({ error: "ticket not found" });
  res.status(200).json(ticket);
});

app.patch("/tickets/:id/status", (req, res) => {
  const ticket = service.moveToNextStatus(req.params.id);
  if (!ticket) return res.status(404).json({ error: "ticket not found" });
  res.status(200).json(ticket);
});

const port = process.env.PORT ?? 3000;
app.listen(port, () =>
  console.log(`TeamBoard backend listening on port ${port}`)
);
```

---

## Checkpoint

`GET /tickets` liefert die Beispieltickets; `PATCH /tickets/:id/status` bewegt ein Ticket einen Status weiter; ein unbekanntes Ticket liefert `404`.

## Projektbezug

Der Server läuft jetzt dauerhaft statt einmalig durchzulaufen - `docker-compose.yml` (Modul 13) braucht dafür eine Port-Freigabe. Weiter geht es mit Lab 14.3: die API im Container testen.
