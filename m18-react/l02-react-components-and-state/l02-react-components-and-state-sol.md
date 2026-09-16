# Lab 18.2 - Lösung: Komponenten und State: Ticket-Karten

## Aufgabe 1-2: `TicketCard` und `Column`

Siehe vollständigen Code im Theorieteil (Lab 18.2, Abschnitte "`TicketCard`-Komponente mit Props" und "`Column`-Komponente mit lokalem State").

## Aufgabe 3: `App.tsx`

```tsx
// sample-react/src/App.tsx
import { Column } from "./components/Column";

function App() {
  return (
    <div style={{ display: "flex", gap: "1rem" }}>
      <Column
        title="To Do"
        initialTickets={[
          { id: "t-1", title: "Login-Formular bauen", assignee: "Alex" },
          { id: "t-2", title: "Datenbank aufsetzen", assignee: "" },
        ]}
      />
      <Column
        title="In Progress"
        initialTickets={[{ id: "t-3", title: "API anbinden", assignee: "Sam" }]}
      />
      <Column title="Done" initialTickets={[]} />
    </div>
  );
}

export default App;
```

## Aufgabe 4: `key`-Prüfung

Jedes Ticket hat eine eindeutige `id` (`t-1`, `t-2`, `t-3`), die als `key` verwendet wird - ohne `key` würde React in der Browser-Konsole eine Warnung ("Each child in a list should have a unique key prop") ausgeben.

## Grenzen

Die Tickets sind weiterhin hartcodiert in `App.tsx` - eine echte Verbindung zur API folgt erst in Modul 19.
