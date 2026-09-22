# Lab 19.5 - Lösung: `useMemo`

## Aufgabe 1-2, 5: `App.tsx` (Ausschnitt)

```tsx
import { useCallback, useEffect, useMemo, useState } from "react";
import { makeDemoTickets } from "./demo-tickets";

// Einmal beim Laden erzeugt - die Objekte bleiben über alle Renderings dieselben
const demoTickets = makeDemoTickets(
  Number(new URLSearchParams(location.search).get("demo") ?? 0)
);

export default function App() {
  const [tickets, setTickets] = useState<Ticket[]>([]);
  const [search, setSearch] = useState("");
  const [showCounts, setShowCounts] = useState(true);
  // ...

  // Teuer bei vielen Tickets: filtern, sortieren, gruppieren.
  // useMemo rechnet nur neu, wenn sich tickets oder search ändern -
  // nicht, wenn App aus einem anderen Grund neu rendert (z. B. showCounts).
  const columns = useMemo(() => {
    const start = performance.now();
    const all = [...tickets, ...demoTickets];
    const needle = search.trim().toLowerCase();
    const groups: Record<Ticket["status"], Ticket[]> = { "To Do": [], "In Progress": [], Done: [] };
    all
      .filter((t) => t.title.toLowerCase().includes(needle))
      .sort((a, b) => a.title.localeCompare(b.title))
      .forEach((t) => groups[t.status].push(t));
    console.log(`columns berechnet: ${(performance.now() - start).toFixed(1)} ms`);
    return groups;
  }, [tickets, search]);

  return (
    // ...
    <div className="d-flex gap-3 align-items-center mb-3">
      <input className="form-control" placeholder="Suchen" value={search}
             onChange={(e) => setSearch(e.target.value)} />
      <label className="form-check-label text-nowrap">
        <input type="checkbox" className="form-check-input me-1" checked={showCounts}
               onChange={(e) => setShowCounts(e.target.checked)} />
        Zähler
      </label>
    </div>
    <div className="row g-3">
      <Column title="To Do" className="todo" tickets={columns["To Do"]} showCount={showCounts} onAdvance={handleAdvance} />
      {/* In Progress, Done analog */}
    </div>
  );
}
```

**Abhängigkeiten:** `tickets` und `search` - beide gehen in die Berechnung ein. `showCounts` gehört **nicht** hinein: Es beeinflusst nur die Anzeige, nicht das Ergebnis. Genau deshalb kann `useMemo` beim Umschalten die Arbeit sparen. `demoTickets` liegt außerhalb der Komponente und ändert sich nie.

## Aufgabe 3-6: Gemessen (09/2026, Production-Build, `?demo=20000`)

| | Zähler 4x umschalten | Suche `a` → `ap` → `api` |
|---|---|---|
| **ohne** `useMemo` | 3.5 / 3.8 / 3.8 / 3.5 ms | 2.2 / 1.3 / 0.6 ms |
| **mit** `useMemo` | **nicht neu berechnet** | 2.7 / 1.3 / 1.0 ms |
| **ohne** `useMemo`, CPU 4x gedrosselt | 16.1 / 15.1 / 15.2 / 15.2 ms | 9.9 / 1.9 / 2.5 ms |
| **mit** `useMemo`, CPU 4x gedrosselt | **nicht neu berechnet** | 9.5 / 2.8 / 1.9 ms |

Nach der Suche `api`: 834 / 833 / 833 Treffer pro Spalte.

**Lesart:**
- Beim Umschalten spart `useMemo` die komplette Berechnung. Auf einem schnellen Rechner sind das 3-4 ms, auf einem vierfach langsameren **15-16 ms - fast das ganze Budget eines Bildes**.
- Beim Tippen bringt `useMemo` nichts: `search` ändert sich, also muss neu gerechnet werden.
- Die Suche wird mit jedem Buchstaben schneller, weil weniger Treffer sortiert werden müssen.

## Aufgabe 7: Bei 3 Tickets?

Nein. Das Filtern und Sortieren von drei Tickets dauert Mikrosekunden - `useMemo` kostet mehr, als es spart, und macht den Code länger. Der Einsatz ist eine Entscheidung auf Basis einer Messung, keine Gewohnheit.

## Commit

```bash
git add -A
git commit -m "feat: Suche und Zähler-Schalter, Spalten per useMemo berechnet"
```

## Grenzen

Die Messzeile (`performance.now()` und `console.log`) gehört nach der Messung wieder heraus - der Linter warnt zu Recht. Wirklich langsam wird ein Board mit 20.000 Tickets ohnehin durch das DOM: Deshalb zeigt jede Spalte höchstens 20 Karten. Die echte Lösung dafür heißt Virtualisierung (nur sichtbare Zeilen rendern) oder Paginierung - wie in Lab 14.7 auf dem Server.
