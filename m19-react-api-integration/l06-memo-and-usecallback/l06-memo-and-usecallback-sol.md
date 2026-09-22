# Lab 19.6 - Lösung: `React.memo` und `useCallback`

## Aufgabe 3: `memo`

```tsx
// frontend/src/components/TicketCard.tsx
import { memo } from "react";
import type { Ticket } from "../api";

interface Props {
  ticket: Ticket;
  onAdvance?: (id: string) => void;
}

// memo: rendert nur neu, wenn sich eine Prop ändert (Vergleich per Referenz)
export const TicketCard = memo(function TicketCard({ ticket, onAdvance }: Props) {
  return (
    <div className="card ticket mb-2">
      {/* ... unverändert ... */}
    </div>
  );
});
```

## Aufgabe 5: `useCallback`

```tsx
// frontend/src/App.tsx (Ausschnitt)
// useCallback: dieselbe Funktion über Renderings hinweg - sonst bekäme
// jede TicketCard bei jedem Rendern von App eine "neue" Prop und memo wäre wirkungslos
const handleAdvance = useCallback(
  async (id: string) => {
    if (!token) return;
    await moveToNextStatus(token, id);
    await loadTickets(token);
  },
  [token, loadTickets]
);
```

`token` und `loadTickets` werden in der Funktion benutzt, also gehören sie ins Array. `loadTickets` ist selbst per `useCallback` mit `[]` stabil, `token` ändert sich nur beim Login.

## Aufgabe 2-6: Gemessen (09/2026, Production-Build, `?demo=20000`, 60 sichtbare Karten)

| Variante | "Zähler" aus | "Zähler" an | Suche `api` |
|---|---|---|---|
| ohne `memo` | 60 | 60 | 60 |
| `memo`, ohne `useCallback` | 40 | 40 | 40 |
| `memo` + `useCallback` | **0** | **0** | **1** |

**Aufgabe 4, die 40:** Die 20 Karten in "Done" haben keinen Button - `Column` gibt ihnen kein `onAdvance` mit. Ihre Props (`ticket`, `onAdvance: undefined`) sind gleich geblieben, `memo` überspringt sie. Die 40 Karten in "To Do" und "In Progress" bekommen bei jedem Rendern ein neues `handleAdvance` - für `memo` eine geänderte Prop.

**Suche `api`, nur 1 Karte:** Die Ticket-Objekte bleiben dieselben (Demo-Tickets außerhalb der Komponente, echte Tickets unverändert im State). Nach dem Filtern stehen fast dieselben Karten oben - nur eine ist neu hinzugekommen.

## Aufgabe 7: Wann ist `useCallback` überflüssig?

- Wenn die Funktion an eine Komponente **ohne** `memo` geht - die rendert ohnehin mit.
- Wenn die Funktion an ein normales HTML-Element geht (`<button onClick={...}>`) - das rendert nicht, React tauscht nur den Handler aus.
- Wenn die Liste so klein ist, dass das Neurendern nichts kostet.

## Commit

```bash
git add -A
git commit -m "perf: TicketCard mit memo, handleAdvance mit useCallback"
```

## Grenzen

Nach einem Klick auf "Weiter →" rendern trotz `memo` alle echten Karten: Die Liste wird neu geladen, und JSON aus dem Netz ergibt immer **neue** Objekte - auch bei gleichem Inhalt. Lab 19.8 ändert das.
