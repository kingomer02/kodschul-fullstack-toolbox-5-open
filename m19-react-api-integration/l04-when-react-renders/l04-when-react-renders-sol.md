# Lab 19.4 - Lösung: Wann rendert React?

## Aufgabe 1: Das leere Board (gemessen 09/2026)

Mit `const [tickets] = useState<Ticket[]>(initialTickets);` in `Column`:

```text
Board nach Login: To Do: - | In Progress: - | Done: -
Ticket-Abrufe:   ["/tickets"]
```

Die Tickets **wurden** geladen - das Board zeigt sie trotzdem nicht. Ablauf:

1. Nach dem Login rendert `App` mit `tickets = []`. Jede `Column` rendert zum ersten Mal, `useState([])` merkt sich die leere Liste.
2. Der `fetch` kommt zurück, `setTickets([...])` → `App` rendert neu, `Column` bekommt volle `initialTickets`.
3. `useState` ignoriert den neuen Anfangswert - er zählt nur beim ersten Rendern. Die Spalte zeigt weiter `[]`.

**Lösung:** kein eigener State in `Column`, sondern direkt die Props anzeigen (so steht es korrigiert in Lab 19.2).

## Aufgabe 2-4: Gemessen (09/2026)

**Production-Build** (`npm run build && npm run preview`) - so oft rendert jede Komponente:

| Aktion | `App` | `NewTicketForm` | je `Column` | je `TicketCard` |
|---|---|---|---|---|
| Laden + Login + Tickets holen | 3 | 2 | 2 | 1 |
| ein Zeichen ins Formular | – | 1 | – | – |
| Klick auf "Weiter →" | 1 | 1 | 1 | 1 |

**Entwicklungsmodus** (`npm run dev`): jede Zahl genau **doppelt** (App 6, Formular 4, …). Ursache: `<StrictMode>` in `main.tsx`.

Die drei Renderings von `App` beim Start: erstes Rendern (Login-Formular) → `setToken` → `setTickets`.

## Aufgabe 5: Erklärung

- **Tastendruck:** Der Titel ist State **in** `NewTicketForm`. Nur diese Komponente ändert ihren State, also rendert nur sie (und ihre Kinder - sie hat keine).
- **"Weiter →":** `App` lädt die Liste neu und ruft `setTickets` auf. `App` rendert neu, und damit **alle** Kinder: jede `Column`, jede `TicketCard`, sogar `NewTicketForm`, obwohl sich für sie nichts geändert hat.

Das ist die Frage für Lab 19.5 und 19.6: Wann ist dieses "alles rendert mit" teuer - und wie verhindert man es gezielt?

## Grenzen

Rendern ist nicht gleich "DOM ändern". Auch wenn alle Karten neu rendern, fasst React im Browser nur die eine Karte an, die sich wirklich geändert hat. Die Kosten liegen in der **JavaScript-Arbeit** der Komponenten-Funktionen - bei drei Karten vernachlässigbar.
