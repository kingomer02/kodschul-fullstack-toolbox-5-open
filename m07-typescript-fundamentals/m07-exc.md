# Transfer-Übung Modul 7 - Übung: Typisierte Beispieldaten mit Auswertung

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - führt Basic Types, Interfaces und typisierte Modelle aus den drei Labs zu einem zusammenhängenden Mini-Feature.

## Ziel

Aus dem isolierten `Ticket`-Interface (Lab 7.3) einen kleinen, tatsächlich nutzbaren Baustein bauen: eine Beispiel-Ticketliste plus eine Funktion, die etwas Sinnvolles damit tut.

## Ausgangslage

- `backend/src/models/ticket.ts` mit dem `Ticket`-Interface aus Lab 7.3 liegt vor.

## Aufgaben

1. Lege `backend/src/data/sample-tickets.ts` an mit einem Array `Ticket[]` mit mindestens 3 Tickets, wobei alle drei Status-Werte mindestens einmal vorkommen.
2. Schreibe in derselben Datei eine Funktion `countByStatus(tickets: Ticket[]): Record<Ticket["status"], number>`, die zählt, wie viele Tickets je Status vorliegen.
3. Rufe `countByStatus` in `index.ts` mit den Beispieldaten auf und logge das Ergebnis.
4. Baue (`npm run build`) und führe (`npm start`) aus; committe bei Erfolg.

## Checkpoint

- `npm start` gibt ein Objekt mit den korrekten Zählwerten je Status aus (z. B. `{ "To Do": 1, "In Progress": 1, "Done": 1 }`).
- `tsc` meldet keine Typfehler.

## Abschlusskriterien

- Typisierte Beispieldaten und eine erste Auswertungsfunktion liegen bereit, um in Modul 8 von `TicketRepository`/`TicketService` verwendet zu werden.

## Fallback

Falls `tsc` einen "not all code paths return a value"-Fehler meldet: sicherstellen, dass `counts` vor der Schleife mit allen drei Status-Schlüsseln initialisiert wird.
