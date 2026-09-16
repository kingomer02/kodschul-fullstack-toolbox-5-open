# Modul 16: Authentifizierung mit JWT

## Lab 16.1 - JWT und OAuth: Grundlagen

---

## Lab-Ziel

Du kennst den Ablauf eines JWT-basierten Logins (Login → Token → geschützte Anfrage) und kannst ihn an einem einfachen Beispielendpunkt nachbauen.

**Leitfragen:**

<details>
<summary>Was steckt grob in einem JWT, und warum kann der Server ihm vertrauen, ohne bei jeder Anfrage in einer Datenbank nachzuschauen?</summary>

Ein JWT enthält Kopfdaten, Nutzdaten (z. B. Nutzername) und eine Signatur, die mit einem geheimen Serverschlüssel erzeugt wurde - der Server kann die Signatur bei jeder Anfrage neu prüfen und erkennt so Manipulationen, ohne den Token-Zustand extra zu speichern.

</details>

<details>
<summary>Wo unterscheidet sich OAuth grundsätzlich von einem klassischen JWT-Login mit Nutzername/Passwort?</summary>

OAuth delegiert die Anmeldung an einen externen Anbieter (z. B. GitHub, Google) statt eigene Zugangsdaten zu prüfen - der eigene Server erhält am Ende trotzdem meist ein Token, verwaltet aber keine Passwörter selbst.

</details>

---

## Minimalbeispiel: Login und geschützte Route

```ts
// sample-auth/src/server.ts
import express from "express";
import jwt from "jsonwebtoken";

const app = express();
app.use(express.json());

const SECRET = "sample-secret-do-not-use-in-production";

app.post("/login", (req, res) => {
  const { username } = req.body;
  if (!username) return res.status(400).json({ error: "username is required" });
  const token = jwt.sign({ username }, SECRET, { expiresIn: "1h" });
  res.status(200).json({ token });
});

function requireAuth(
  req: express.Request,
  res: express.Response,
  next: express.NextFunction
) {
  const header = req.headers.authorization;
  if (!header?.startsWith("Bearer ")) {
    return res.status(401).json({ error: "missing token" });
  }
  try {
    jwt.verify(header.slice("Bearer ".length), SECRET);
    next();
  } catch {
    res.status(401).json({ error: "invalid token" });
  }
}

app.get("/profile", requireAuth, (req, res) => {
  res.status(200).json({ message: "you are authenticated" });
});

app.listen(3100, () => console.log("Sample auth API on port 3100"));
```

---

## Ablauf

1. `POST /login` mit `{"username": "sam"}` liefert einen Token.
2. `GET /profile` **ohne** `Authorization`-Header liefert `401`.
3. `GET /profile` **mit** `Authorization: Bearer <token>` liefert `200`.

---

## Checkpoint

Eine Anfrage ohne gültigen Token an eine geschützte Route liefert zuverlässig `401`; mit gültigem Token liefert dieselbe Route `200`.

Weiter geht es mit Lab 16.2: der Login-Flow für TeamBoard.
