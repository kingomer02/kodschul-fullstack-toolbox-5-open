# Lab 19.3 - Lösung: Vertiefende Übung: Aktionen aus der Oberfläche auslösen

## Aufgabe 1-2: `TicketCard` und `NewTicketForm`

Siehe vollständigen Code im Theorieteil (Lab 19.3, Abschnitte "Status-Button auf `TicketCard`" und "Neues Ticket anlegen").

## Aufgabe 3-4: `App.tsx` mit `loadTickets`

```tsx
// frontend/src/App.tsx (Ausschnitt)
function App() {
  const [token, setToken] = useState<string | null>(null);
  const [tickets, setTickets] = useState<Ticket[]>([]);

  function loadTickets(currentToken: string) {
    fetch("http://localhost:3000/tickets", {
      headers: { Authorization: `Bearer ${currentToken}` },
    })
      .then((res) => res.json())
      .then(setTickets);
  }

  useEffect(() => {
    if (token) loadTickets(token);
  }, [token]);

  if (!token) return <LoginForm onLoggedIn={setToken} />;

  return (
    <div className="container-fluid">
      <NewTicketForm token={token} onCreated={() => loadTickets(token)} />
      {/* Spalten wie in Lab 19.2, TicketCard erhält zusätzlich token und onChanged */}
    </div>
  );
}
```

## Aufgabe 5-6: Testen

Neues Ticket per Formular anlegen → erscheint sofort in "To Do". Klick auf "Weiter →" → Ticket wechselt sichtbar in "In Progress".

## Aufgabe 7: Commit

```bash
git add -A
git commit -m "feat: wire create/move-status actions in the React frontend"
```

## Grenzen

Jede Aktion lädt die komplette Ticketliste neu, statt nur das betroffene Ticket lokal zu aktualisieren - für die Kursgröße ausreichend performant, bei sehr vielen Tickets wäre eine gezieltere State-Aktualisierung sinnvoller.
