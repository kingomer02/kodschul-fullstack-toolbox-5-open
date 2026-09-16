# Modul 16: Authentifizierung mit JWT

## Lab 16.3 - Geschützte Routen testen

---

## Lab-Ziel

Du sicherst alle bestehenden `/tickets`-Routen mit der `requireAuth`-Middleware ab und bestätigst systematisch, dass unauthentifizierte Anfragen abgelehnt und authentifizierte Anfragen weiterhin funktionieren.

**Leitfragen:**

<details>
<summary>Warum reicht ein einziger `app.use("/tickets", requireAuth)`-Aufruf, statt die Middleware bei jeder einzelnen Route zu wiederholen?</summary>

Express wendet eine mit `app.use(pfad, middleware)` registrierte Middleware auf alle Routen an, die mit diesem Pfad beginnen - ein zentraler Aufruf deckt `GET`, `POST` und `PATCH` unter `/tickets` gleichermaßen ab.

</details>

<details>
<summary>Warum muss die Middleware **vor** den eigentlichen Routen-Definitionen registriert werden?</summary>

Express verarbeitet Middleware und Routen in der Reihenfolge ihrer Registrierung - würde `requireAuth` erst nach den Routen stehen, würden Anfragen die Routen bereits ungeprüft erreichen.

</details>

---

## `/tickets` absichtlich absichern

```ts
// backend/src/index.ts (Ergänzung, vor den /tickets-Routen)
import { requireAuth } from "./auth/require-auth";

app.use("/tickets", requireAuth);

app.get("/tickets", async (req, res) => {
  // ... unverändert
});
```

- Alle bisherigen `/tickets`-Routen aus Modul 14/15 bleiben inhaltlich unverändert - nur die vorgeschaltete Middleware ist neu.

---

## Systematisch testen

```bash
# 1. Ohne Token
curl -i http://localhost:3000/tickets
# HTTP/1.1 401

# 2. Login, um einen Token zu erhalten
TOKEN=$(curl -s -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username": "alex", "password": "hunter2"}' | jq -r .token)

# 3. Mit gültigem Token
curl -i http://localhost:3000/tickets -H "Authorization: Bearer $TOKEN"
# HTTP/1.1 200

# 4. Mit ungültigem Token
curl -i http://localhost:3000/tickets -H "Authorization: Bearer offensichtlich-falsch"
# HTTP/1.1 401
```

---

## Checkpoint

Schritt 1 und 4 liefern `401`; Schritt 3 liefert `200` mit der Ticketliste - dieselbe Prüfung funktioniert für alle `/tickets`-Routen (`GET`, `POST`, `PATCH`).

## Projektbezug

Die REST-API ist jetzt vollständig durch Login abgesichert. Modul 17 widmet sich der visuellen Gestaltung der Kanban-Oberfläche, die diese API später konsumiert.
