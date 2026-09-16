# Modul 19: React trifft die gesicherte API

## Lab 19.3 - Vertiefende Übung: Aktionen aus der Oberfläche auslösen

---

## Lab-Ziel

Du ergänzt Buttons auf den Ticket-Karten, die echte `POST`/`PATCH`-Anfragen auslösen (Ticket anlegen, Status weiterbewegen) und das Board danach automatisch aktualisieren.

**Leitfragen:**

<details>
<summary>Warum muss nach einer erfolgreichen `PATCH`-Anfrage die Ticketliste im Frontend neu geladen werden?</summary>

Der React-State im Browser kennt nur den Stand zum Zeitpunkt des letzten Ladens - eine Änderung in der Datenbank wird der Oberfläche nicht automatisch bekannt, ohne die Daten erneut abzurufen.

</details>

<details>
<summary>Warum ist ein einzelner `refreshTickets`-Aufruf nach jeder Aktion einfacher als das State-Array manuell an einer Stelle zu verändern?</summary>

Ein erneuter Abruf garantiert, dass das Frontend exakt den tatsächlichen Datenbankstand zeigt, statt riskante Annahmen über den neuen Zustand einzelner Felder im Frontend selbst zu treffen.

</details>

---

## Status-Button auf `TicketCard`

```tsx
// frontend/src/components/TicketCard.tsx (erweitert)
interface TicketCardProps {
  id: string;
  title: string;
  assignee: string;
  token: string;
  onChanged: () => void;
}

export function TicketCard({
  id,
  title,
  assignee,
  token,
  onChanged,
}: TicketCardProps) {
  async function moveNext() {
    await fetch(`http://localhost:3000/tickets/${id}/status`, {
      method: "PATCH",
      headers: { Authorization: `Bearer ${token}` },
    });
    onChanged();
  }

  return (
    <div className="card mb-2">
      <div className="card-body">
        <p className="mb-1">{title}</p>
        <small className="text-muted">{assignee || "Nicht zugewiesen"}</small>
        <div>
          <button
            className="btn btn-sm btn-outline-primary mt-2"
            onClick={moveNext}
          >
            Weiter →
          </button>
        </div>
      </div>
    </div>
  );
}
```

## Neues Ticket anlegen

```tsx
// frontend/src/components/NewTicketForm.tsx
import { useState } from "react";

interface NewTicketFormProps {
  token: string;
  onCreated: () => void;
}

export function NewTicketForm({ token, onCreated }: NewTicketFormProps) {
  const [title, setTitle] = useState("");

  async function handleSubmit(e: React.FormEvent) {
    e.preventDefault();
    await fetch("http://localhost:3000/tickets", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${token}`,
      },
      body: JSON.stringify({ title }),
    });
    setTitle("");
    onCreated();
  }

  return (
    <form onSubmit={handleSubmit} className="mb-3">
      <input
        value={title}
        onChange={(e) => setTitle(e.target.value)}
        placeholder="Neues Ticket"
      />
      <button type="submit">Anlegen</button>
    </form>
  );
}
```

## Ticketliste nach Aktionen neu laden

```tsx
// frontend/src/App.tsx (Ausschnitt, Ergänzung)
function loadTickets(token: string) {
  fetch("http://localhost:3000/tickets", {
    headers: { Authorization: `Bearer ${token}` },
  })
    .then((res) => res.json())
    .then(setTickets);
}

// im JSX:
<NewTicketForm token={token} onCreated={() => loadTickets(token)} />;
```

- `TicketCard` erhält jetzt zusätzlich `token` und `onChanged={() => loadTickets(token)}` als Props von `Column`/`App` weitergereicht.

---

## Checkpoint

Ein Klick auf "Weiter →" bewegt ein Ticket sichtbar in die nächste Spalte; ein neu über das Formular angelegtes Ticket erscheint sofort in "To Do" - beides ohne manuelles Neuladen der Browserseite.

## Projektbezug

Damit ist der komplette TeamBoard-Fluss (Login → Board laden → Ticket anlegen/verschieben) vollständig über die React-Oberfläche nutzbar. Modul 20 zeigt Angular als Vergleichsalternative zu React.
