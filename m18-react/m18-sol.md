# Transfer-Übung Modul 18 - Lösung: Vierte Spalte als eigenständige Komponentenübung

## Aufgabe 1: Beispieldaten

```ts
// frontend/src/data/sample-tickets.ts (testweise Ergänzung)
export const sampleTickets = {
  todo: [{ id: "t-1", title: "Login-Formular bauen", assignee: "Alex" }],
  inProgress: [{ id: "t-2", title: "API anbinden", assignee: "Sam" }],
  done: [],
  blocked: [{ id: "t-4", title: "Warten auf Freigabe", assignee: "" }],
};
```

## Aufgabe 2-3: `App.tsx` mit vierter Spalte

```tsx
<div className="row">
  <div className="col-12 col-md-3 column todo">
    <Column title="To Do" initialTickets={sampleTickets.todo} />
  </div>
  <div className="col-12 col-md-3 column in-progress">
    <Column title="In Progress" initialTickets={sampleTickets.inProgress} />
  </div>
  <div className="col-12 col-md-3 column done">
    <Column title="Done" initialTickets={sampleTickets.done} />
  </div>
  <div className="col-12 col-md-3 column blocked">
    <Column title="Blocked" initialTickets={sampleTickets.blocked} />
  </div>
</div>
```

Alle vier Spalten rendern korrekt, ohne dass `Column.tsx` oder `TicketCard.tsx` angepasst werden mussten.

## Aufgabe 4-5: Zurücksetzen

```bash
git checkout -- .
git status
# nothing to commit, working tree clean
```

## Grenzen

TeamBoard verwendet offiziell nur die drei Status `To Do`, `In Progress`, `Done` (Modul 7/8) - "Blocked" ist bewusst nur eine temporäre Übungsspalte und kein Teil des Datenmodells.
