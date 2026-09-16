# Transfer-Übung Modul 8 - Übung: End-to-End-Ablauf mit Repository und Service

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - schließt den Tag-2-Meilenstein (Node.js + TypeScript-Backend mit typisierten Modellen und OOP-Struktur) ab.

## Ziel

`Repository<T>`, `TicketRepository` und `TicketService` aus den drei Labs nicht nur isoliert testen, sondern zu einem einzigen, sichtbaren End-to-End-Ablauf verbinden.

## Ausgangslage

- `backend/src/repositories/repository.ts`, `ticket-repository.ts` und `backend/src/services/ticket-service.ts` aus Lab 8.1-8.3 liegen vor.
- `backend/src/data/sample-tickets.ts` aus der Modul-7-Transfer-Übung liegt vor.

## Aufgaben

1. Instanziiere in `index.ts` eine `TicketRepository` und befülle sie mit den Beispieltickets aus `sample-tickets.ts` (über `add`).
2. Instanziiere einen `TicketService` mit diesem Repository.
3. Rufe `moveToNextStatus` für ein Ticket mit Status `To Do` zweimal auf und logge den Status vor jedem Aufruf und danach.
4. Baue und teste lokal (`npm run build && npm start`), committe und pushe - die CI-Pipeline muss grün bleiben.

## Checkpoint

- Die Konsolenausgabe zeigt den Übergang `To Do -> In Progress -> Done` für das gewählte Ticket.
- CI-Check auf `main` bleibt grün.

## Abschlusskriterien

- Der Tag-2-Backend-Meilenstein (Node.js, TypeScript, typisierte Modelle, OOP-Repository/Service) ist vollständig lauffähig - Grundlage für die Container-Themen ab Modul 11.

## Fallback

Falls `findById` `undefined` liefert: prüfen, ob die IDs in `sample-tickets.ts` (`t-1`, `t-2`, `t-3`) exakt mit der abgefragten ID übereinstimmen.
