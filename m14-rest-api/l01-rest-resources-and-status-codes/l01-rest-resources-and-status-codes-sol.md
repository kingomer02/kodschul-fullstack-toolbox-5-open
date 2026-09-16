# Lab 14.1 - Lösung: Ressourcen, HTTP-Methoden und Statuscodes

## Aufgabe 1: `server.ts`

```ts
// sample-api/src/server.ts
import express from "express";

const app = express();
app.use(express.json());

interface Item {
  id: string;
  name: string;
}

const items: Item[] = [];

app.get("/items", (req, res) => {
  res.status(200).json(items);
});

app.post("/items", (req, res) => {
  const { name } = req.body;
  if (!name) {
    return res.status(400).json({ error: "name is required" });
  }
  const item: Item = { id: String(items.length + 1), name };
  items.push(item);
  res.status(201).json(item);
});

app.listen(3000, () => console.log("Sample API listening on port 3000"));
```

## Aufgabe 2-4: Testen

```bash
curl http://localhost:3000/items
# []

curl -X POST http://localhost:3000/items \
  -H "Content-Type: application/json" \
  -d '{"name": "test"}'
# 201 { "id": "1", "name": "test" }

curl http://localhost:3000/items
# [{ "id": "1", "name": "test" }]

curl -X POST http://localhost:3000/items \
  -H "Content-Type: application/json" \
  -d '{}'
# 400 { "error": "name is required" }
```

## Grenzen

Die Daten leben nur im Arbeitsspeicher - ein Neustart des Servers leert `items` wieder.
