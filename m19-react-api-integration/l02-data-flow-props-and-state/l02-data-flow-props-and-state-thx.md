# Modul 19: React trifft die gesicherte API

## Lab 19.2 - Datenfluss: Login, Token und echte Tickets laden

---

## Lab-Ziel

Du baust einen Login-Formular-Fluss, der den JWT-Token aus Modul 16 im React-State hält, und lädst damit echte Tickets von der REST-API statt der hartcodierten Beispieldaten aus Modul 18.

**Leitfragen:**

<details>
<summary>Warum wird der Token im State (und optional `localStorage`) gehalten, statt ihn bei jeder Anfrage neu einzugeben?</summary>

Ein einmal erhaltener Token bleibt für seine Gültigkeitsdauer nutzbar - ihn zwischenzuspeichern erspart, sich bei jeder einzelnen Anfrage erneut einzuloggen.

</details>

<details>
<summary>Warum braucht die Backend-Express-App jetzt CORS-Unterstützung (`cors`-Paket)?</summary>

Frontend (`http://localhost:5173`, Vite) und Backend (`http://localhost:3000`) laufen auf unterschiedlichen Ursprüngen (Origins) - ohne CORS-Header blockt der Browser die Antwort des Backends aus Sicherheitsgründen.

</details>

---

## CORS im Backend aktivieren

```bash
cd backend
npm install cors
npm install --save-dev @types/cors
```

```ts
// backend/src/index.ts (Ergänzung, vor den Routen)
import cors from "cors";

app.use(cors());
```

**Grenze:** `cors()` ohne Optionen erlaubt in dieser Kursumgebung bewusst alle Ursprünge - für eine echte Produktionsumgebung würde man `origin` auf die tatsächliche Frontend-Domain einschränken.

---

## Login-Formular mit State

```tsx
// frontend/src/components/LoginForm.tsx
import { useState } from "react";

interface LoginFormProps {
  onLoggedIn: (token: string) => void;
}

export function LoginForm({ onLoggedIn }: LoginFormProps) {
  const [username, setUsername] = useState("");
  const [password, setPassword] = useState("");
  const [error, setError] = useState("");

  async function handleSubmit(e: React.FormEvent) {
    e.preventDefault();
    const res = await fetch("http://localhost:3000/auth/login", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ username, password }),
    });
    if (!res.ok) {
      setError("Anmeldung fehlgeschlagen");
      return;
    }
    const data = await res.json();
    onLoggedIn(data.token);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={username}
        onChange={(e) => setUsername(e.target.value)}
        placeholder="Nutzername"
      />
      <input
        value={password}
        onChange={(e) => setPassword(e.target.value)}
        type="password"
        placeholder="Passwort"
      />
      <button type="submit">Anmelden</button>
      {error && <p className="text-danger">{error}</p>}
    </form>
  );
}
```

## Echte Tickets laden

```tsx
// frontend/src/App.tsx
import { useEffect, useState } from "react";
import { LoginForm } from "./components/LoginForm";
import { Column } from "./components/Column";

interface Ticket {
  id: string;
  title: string;
  assignee: string;
  status: "To Do" | "In Progress" | "Done";
}

function App() {
  const [token, setToken] = useState<string | null>(null);
  const [tickets, setTickets] = useState<Ticket[]>([]);

  useEffect(() => {
    if (!token) return;
    fetch("http://localhost:3000/tickets", {
      headers: { Authorization: `Bearer ${token}` },
    })
      .then((res) => res.json())
      .then(setTickets);
  }, [token]);

  if (!token) {
    return <LoginForm onLoggedIn={setToken} />;
  }

  return (
    <div className="container-fluid">
      <div className="row">
        <div className="col-12 col-md-4 column todo">
          <Column
            title="To Do"
            initialTickets={tickets.filter((t) => t.status === "To Do")}
          />
        </div>
        <div className="col-12 col-md-4 column in-progress">
          <Column
            title="In Progress"
            initialTickets={tickets.filter((t) => t.status === "In Progress")}
          />
        </div>
        <div className="col-12 col-md-4 column done">
          <Column
            title="Done"
            initialTickets={tickets.filter((t) => t.status === "Done")}
          />
        </div>
      </div>
    </div>
  );
}

export default App;
```

- Solange `token` `null` ist, zeigt `App` nur das Login-Formular - erst nach erfolgreichem Login (`onLoggedIn`) lädt `useEffect` echte Tickets nach.

---

## Checkpoint

Nach einem erfolgreichen Login im Formular erscheint das Board mit echten, aus MongoDB geladenen Tickets statt der hartcodierten Beispieldaten aus Modul 18.

## Projektbezug

Weiter geht es mit Lab 19.3: Aktionen (Ticket anlegen, zuweisen, Status ändern) direkt aus der Oberfläche heraus auslösen.
