# Lab 14.2 - Übung: Express-REST-API für TeamBoard

**Dauer:** ca. 45 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - macht das Backend zu einem echten, dauerhaft laufenden HTTP-Server.

## Ausgangslage

- `TicketRepository`/`TicketService`/`sample-tickets.ts` aus Modul 7/8 liegen vor.
- `npm install express` und `npm install --save-dev @types/express` sind im `backend/`-Ordner noch nicht ausgeführt.

## Aufgaben

1. Installiere `express` und `@types/express` im `backend/`-Ordner.
2. Ergänze `Repository<T>` um eine Methode `getAll(): T[]`.
3. Ergänze `TicketService` um eine Methode `assign(id: string, assignee: string): Ticket | undefined`.
4. Baue `backend/src/index.ts` zu einem Express-Server um mit den Routen `GET /tickets`, `GET /tickets/:id`, `POST /tickets`, `PATCH /tickets/:id/assign`, `PATCH /tickets/:id/status` (siehe Statuscodes aus Lab 14.1: `200`, `201`, `400`, `404`).
5. Starte den Server lokal (`npm run build && npm start`) und teste alle fünf Routen mit `curl`.
6. Committe die Änderungen.

## Checkpoint

- `GET /tickets` liefert die Beispieltickets aus Modul 7.

> **Korrektur (Durchlauf 09/2026, Ö. Akgeyik):** Das Original spricht von „den drei Beispieltickets aus Modul 7“ - dort sind es **zwei**. Entweder ihr ergänzt in Modul 7 ein drittes Ticket, oder ihr erwartet hier zwei. Wichtig ist nur, dass beide Stellen dieselbe Zahl nennen.
- `PATCH /tickets/t-1/status` bewegt das Ticket sichtbar einen Status weiter.
- `GET /tickets/unbekannte-id` liefert Status `404`.

## Abschlusskriterien

- Der Server läuft dauerhaft (`app.listen`), bis er manuell beendet wird - kein einmalig durchlaufendes Skript mehr.

## Fallback

Falls Port 3000 bereits belegt ist: `PORT=3001 npm start` verwenden (der Code liest `process.env.PORT`).
