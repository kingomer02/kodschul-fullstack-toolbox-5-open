# Modul 16: Authentifizierung mit JWT

## Lab 16.2 - Login-Flow für TeamBoard implementieren

---

## Lab-Ziel

Du baust Registrierung und Login für TeamBoard mit gehashten Passwörtern und JWT-Tokens, als eigenständiges Auth-Modul neben der bestehenden Ticket-Logik.

**Leitfragen:**

<details>
<summary>Warum wird das Passwort mit `bcrypt` gehasht, statt es im Klartext zu speichern?</summary>

Bei einem Datenbank-Leck wären Klartext-Passwörter sofort für alle Konten nutzbar; ein Hash lässt sich praktisch nicht in vertretbarer Zeit zurückrechnen, sodass gestohlene Hashes allein nicht ausreichen, um sich anzumelden.

</details>

<details>
<summary>Warum liegt `JWT_SECRET` in einer Umgebungsvariable statt fest im Code?</summary>

Ein im Code fest hinterlegtes Geheimnis würde mit jedem Blick in den Quellcode (z. B. auf GitHub) offengelegt - eine Umgebungsvariable hält es getrennt vom Code und pro Umgebung austauschbar.

</details>

---

## Nutzerverwaltung und Login-Routen

```bash
cd backend
npm install bcrypt jsonwebtoken
npm install --save-dev @types/bcrypt @types/jsonwebtoken
```

```ts
// backend/src/auth/users.ts
export interface User {
  username: string;
  passwordHash: string;
}

export const users: User[] = [];
```

```ts
// backend/src/auth/auth-routes.ts
import { Router } from "express";
import bcrypt from "bcrypt";
import jwt from "jsonwebtoken";
import { users } from "./users";

const router = Router();
const JWT_SECRET = process.env.JWT_SECRET ?? "dev-only-secret";

router.post("/register", async (req, res) => {
  const { username, password } = req.body;
  if (!username || !password) {
    return res
      .status(400)
      .json({ error: "username and password are required" });
  }
  if (users.some((u) => u.username === username)) {
    return res.status(400).json({ error: "username already taken" });
  }
  const passwordHash = await bcrypt.hash(password, 10);
  users.push({ username, passwordHash });
  res.status(201).json({ username });
});

router.post("/login", async (req, res) => {
  const { username, password } = req.body;
  const user = users.find((u) => u.username === username);
  if (!user || !(await bcrypt.compare(password, user.passwordHash))) {
    return res.status(401).json({ error: "invalid credentials" });
  }
  const token = jwt.sign({ username }, JWT_SECRET, { expiresIn: "1h" });
  res.status(200).json({ token });
});

export default router;
```

```ts
// backend/src/index.ts (Ergänzung)
import authRoutes from "./auth/auth-routes";

app.use("/auth", authRoutes);
```

---

## Middleware für geschützte Routen

```ts
// backend/src/auth/require-auth.ts
import { NextFunction, Request, Response } from "express";
import jwt from "jsonwebtoken";

const JWT_SECRET = process.env.JWT_SECRET ?? "dev-only-secret";

export function requireAuth(req: Request, res: Response, next: NextFunction) {
  const header = req.headers.authorization;
  if (!header?.startsWith("Bearer ")) {
    return res.status(401).json({ error: "missing token" });
  }
  try {
    jwt.verify(header.slice("Bearer ".length), JWT_SECRET);
    next();
  } catch {
    res.status(401).json({ error: "invalid token" });
  }
}
```

---

## Checkpoint

`POST /auth/register` legt einen Nutzer an; `POST /auth/login` mit denselben Zugangsdaten liefert einen Token; ein Login mit falschem Passwort liefert `401`.

## Projektbezug

Der Token aus `/auth/login` wird in Lab 16.3 genutzt, um die bestehenden `/tickets`-Routen abzusichern.
