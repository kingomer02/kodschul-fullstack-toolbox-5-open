# Lab 16.3 - Lösung: Geschützte Routen testen

## Aufgabe 1: Middleware registrieren

```ts
// backend/src/index.ts (Ausschnitt)
import { requireAuth } from "./auth/require-auth";

app.use("/tickets", requireAuth);

app.get("/tickets", async (req, res) => {
  res.status(200).json(await repository.getAll());
});
// ... restliche /tickets-Routen unverändert
```

## Aufgabe 2: Neu bauen und starten

```bash
docker compose up -d --build
```

## Aufgabe 3: Ohne Token

```bash
curl -i http://localhost:3000/tickets
# HTTP/1.1 401
```

## Aufgabe 4: Login

```bash
TOKEN=$(curl -s -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username": "alex", "password": "hunter2"}' | jq -r .token)
```

## Aufgabe 5: Mit gültigem Token

```bash
curl -i http://localhost:3000/tickets -H "Authorization: Bearer $TOKEN"
# HTTP/1.1 200

curl -i -X POST http://localhost:3000/tickets \
  -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
  -d '{"title": "Geschütztes Ticket"}'
# HTTP/1.1 201

curl -i -X PATCH http://localhost:3000/tickets/<id>/status \
  -H "Authorization: Bearer $TOKEN"
# HTTP/1.1 200
```

## Aufgabe 6: Falscher Token

```bash
curl -i http://localhost:3000/tickets -H "Authorization: Bearer offensichtlich-falsch"
# HTTP/1.1 401
```

## Aufgabe 7: Commit

```bash
git add -A
git commit -m "feat: protect ticket routes with JWT auth"
```

## Grenzen

`/auth/register` und `/auth/login` bleiben bewusst ungeschützt - ohne diese beiden offenen Routen könnte sich niemand einloggen, um überhaupt einen Token zu bekommen.
