# Lab 15.3 - Lösung: MongoDB-Integration für TeamBoard

## Aufgabe 1: Installation

```bash
cd backend
npm install mongodb @apollo/server @as-integrations/express4 graphql graphql-tag
```

## Aufgabe 2: `TicketRepository` mit MongoDB

Siehe vollständigen Code im Theorieteil (Lab 15.3, Abschnitt "MongoDB-Treiber einbinden").

## Aufgabe 3: Routen anpassen

```ts
// backend/src/index.ts (Ausschnitt, Ergänzung um await)
app.get("/tickets", async (req, res) => {
  res.status(200).json(await repository.getAll());
});

app.get("/tickets/:id", async (req, res) => {
  const ticket = await repository.findById(req.params.id);
  if (!ticket) return res.status(404).json({ error: "ticket not found" });
  res.status(200).json(ticket);
});

app.post("/tickets", async (req, res) => {
  const { title, description, assignee } = req.body;
  if (!title) return res.status(400).json({ error: "title is required" });
  const ticket = {
    id: `t-${Date.now()}`,
    title,
    description: description ?? "",
    assignee: assignee ?? "",
    status: "To Do" as const,
  };
  await repository.add(ticket);
  res.status(201).json(ticket);
});
```

## Aufgabe 4-5: GraphQL-Schema und Einhängen

Siehe vollständigen Code im Theorieteil (Abschnitte "GraphQL-Schema für Tickets" und die Ergänzung in `index.ts`).

## Aufgabe 6: Testen im Playground

```graphql
query {
  tickets {
    id
    title
    status
  }
}

mutation {
  createTicket(title: "GraphQL-Ticket") {
    id
    status
  }
}
```

## Aufgabe 7: Persistenz prüfen

```bash
docker compose restart backend
# erneute tickets-Query zeigt weiterhin alle Tickets, inkl. des per GraphQL angelegten
```

## Aufgabe 8: Commit

```bash
git add -A
git commit -m "feat: connect backend to MongoDB and add GraphQL API"
```

## Grenzen

Es gibt noch keinen Zugriffsschutz - jede Person mit Netzwerkzugriff auf den Container kann Tickets lesen und anlegen. Das behebt Modul 16 mit JWT-Authentifizierung.
