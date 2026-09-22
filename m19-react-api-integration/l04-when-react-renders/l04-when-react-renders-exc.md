# Lab 19.4 - Übung: Wann rendert React?

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - Messung mit vorübergehenden Log-Zeilen, die danach wieder entfernt werden.

## Ausgangslage

- Das Board aus Lab 19.3: Login, echte Tickets, "Weiter →" und neues Ticket anlegen funktionieren.

## Aufgaben

1. **Das leere Board.** Baue in einer Kopie von `Column` kurz die Fassung aus Lab 18.2 nach: Die Tickets kommen als `initialTickets` herein und werden per `useState(initialTickets)` übernommen. Melde dich an. Was siehst du - und warum? Danach zurück zur Props-Fassung.
2. Setz in `App`, `Column`, `TicketCard` und `NewTicketForm` jeweils ganz oben eine Zeile `console.count("render <Name>")`.
3. **Vorhersage zuerst, dann messen.** Schreib auf, welche Komponenten wie oft rendern, wenn du (a) die Seite lädst und dich anmeldest, (b) ein Zeichen ins Formular "Neues Ticket" tippst, (c) auf "Weiter →" klickst. Dann in der Browser-Konsole prüfen.
4. Die Zahlen sind doppelt so hoch wie erwartet? Finde die Ursache in `main.tsx`. Bestätige sie mit einem Production-Build: `npm run build` und `npm run preview`.
5. Erkläre mit den Regeln aus dem Theorieteil, warum ein Tastendruck im Formular **nur** das Formular neu rendert, ein Klick auf "Weiter →" aber alles.
6. Entferne die Log-Zeilen wieder.

## Checkpoint

- Du kannst erklären, warum das Board mit `useState(initialTickets)` leer bleibt.
- Deine Vorhersage aus Aufgabe 3 stimmt mit der Messung im Production-Build überein.

## Abschlusskriterien

- Du kannst die drei Auslöser für ein neues Rendering nennen.
- Du kannst sagen, warum Props **allein** kein Rendering auslösen.

## Fallback

Falls die Konsole zu voll wird: In den Entwicklertools nach `render` filtern. `console.count` zählt pro Text getrennt.
