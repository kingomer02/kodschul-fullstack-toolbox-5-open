# Lab 19.5 - Übung: `useMemo`

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - das Board bekommt eine Suche und einen Schalter für die Spaltenzähler.

## Ausgangslage

- Das Board aus Lab 19.3, Erkenntnisse aus Lab 19.4.

## Messaufbau (vorgegeben - nicht das Lernziel)

Damit es etwas zu messen gibt, braucht das Board viele Tickets. Lege `src/demo-tickets.ts` an:

```ts
import type { Ticket } from "./api";   // bzw. dort, wo dein Ticket-Typ liegt

// Nur für die Messung: viele Tickets ohne Datenbank. Aufruf mit ?demo=20000
const words = ["API", "backup", "Login", "deploy", "Cache", "report", "Suche", "export"];
const statuses: Ticket["status"][] = ["To Do", "In Progress", "Done"];

export function makeDemoTickets(count: number): Ticket[] {
  return Array.from({ length: count }, (_, i) => ({
    id: `demo-${i}`,
    title: `${words[i % words.length]} ${words[(i * 7) % words.length]} #${i}`,
    description: "",
    assignee: i % 3 === 0 ? "Alex" : "Sam",
    status: statuses[i % 3],
  }));
}
```

Und außerhalb der `App`-Komponente, **einmal** beim Laden:

```ts
const demoTickets = makeDemoTickets(Number(new URLSearchParams(location.search).get("demo") ?? 0));
```

Damit nicht 20.000 Karten im Browser landen: `Column` zeigt höchstens 20 Karten und darunter "… und N weitere".

## Aufgaben

1. Ergänze in `App` ein **Suchfeld** (filtert nach Titel, ohne Groß-/Kleinschreibung) und eine Checkbox **"Zähler"**, die die Anzahl im Spaltenkopf ein- und ausblendet.
2. Berechne die drei Spalten in **einem** Schritt: echte Tickets plus Demo-Tickets, nach Suchbegriff filtern, nach Titel sortieren, nach Status gruppieren. Miss die Dauer mit `performance.now()` und gib sie in der Konsole aus.
3. **Ohne `useMemo` messen**, im Production-Build mit `?demo=20000`: Wie lange dauert die Berechnung beim Umschalten von "Zähler"? Und beim Tippen in die Suche?
4. Dieselbe Messung mit **4-facher CPU-Drosselung** (DevTools → Performance → Zahnrad → CPU).
5. Pack die Berechnung in `useMemo`. Welche Abhängigkeiten gehören hinein - und welche ausdrücklich nicht?
6. Miss erneut. Was ändert sich beim Umschalten, was beim Tippen?
7. Entscheide und begründe: Würdest du `useMemo` hier auch bei 3 Tickets einsetzen?

## Checkpoint

- Mit `useMemo` erscheint beim Umschalten von "Zähler" **keine** Messzeile mehr in der Konsole.
- Beim Tippen in die Suche wird weiterhin gerechnet.

## Abschlusskriterien

- Du kannst mit deinen eigenen Zahlen begründen, ab wann sich `useMemo` hier lohnt.
- Du kannst erklären, warum `showCounts` **nicht** ins Abhängigkeitsarray gehört.

## Fallback

Falls die Suche nichts findet: `includes` ist case-sensitiv - Titel **und** Suchbegriff klein machen.

## Hinweis zum Linter

`npm run lint` warnt bei `performance.now()` im Rendern (`react(purity)`). Zu Recht: Messcode gehört nur während der Messung in die Komponente.
