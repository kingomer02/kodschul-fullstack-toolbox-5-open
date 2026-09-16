# Lab 18.2 - Übung: Komponenten und State: Ticket-Karten

**Dauer:** ca. 40 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - erste React-Komponenten für TeamBoard (noch ohne echtes Vite-Projekt-Setup, das folgt in Lab 18.3).

## Vorbereitung

- Dasselbe `sample-react`-Vite-Projekt aus Lab 18.1 kann für diese Übung weiterverwendet werden.

## Aufgaben

1. Erstelle eine `TicketCard`-Komponente, die `title` und `assignee` als Props entgegennimmt und als Bootstrap-`card` rendert (falls Bootstrap-CSS noch nicht eingebunden ist: einfaches HTML ohne Bootstrap-Klassen reicht für diese Übung).
2. Erstelle eine `Column`-Komponente, die `title` und ein Array `initialTickets` als Props entgegennimmt, dieses Array per `useState` in lokalen State übernimmt und für jedes Element eine `TicketCard` rendert.
3. Rendere in `App.tsx` drei `Column`-Komponenten ("To Do", "In Progress", "Done") mit jeweils 1-3 hartcodierten Beispieltickets.
4. Prüfe, dass jedes Ticket einen eindeutigen `key` erhält (z. B. über eine `id`), und erkläre, was ohne `key` passieren würde (React würde eine Warnung in der Konsole ausgeben).

## Checkpoint

- Alle drei Spalten rendern die jeweils übergebenen Ticket-Titel und Zuweisungen korrekt.
- Die Browser-Konsole zeigt keine "missing key"-Warnung.

## Abschlusskriterien

- Du kannst erklären, warum `initialTickets` als Prop hereinkommt, aber `tickets` als eigener State innerhalb von `Column` verwaltet wird (Vorbereitung für spätere Änderungen wie Drag-and-drop, hier nicht Teil der Übung).

## Fallback

Falls TypeScript-Fehler bei den Props auftreten: `interface`-Definitionen exakt wie im Theorieteil übernehmen und auf korrekte Groß-/Kleinschreibung der Feldnamen achten.
