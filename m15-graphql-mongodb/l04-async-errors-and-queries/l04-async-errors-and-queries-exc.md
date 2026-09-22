# Lab 15.4 - Übung: async-Fehler abfangen und Abfragen in die Datenbank verlegen

**Dauer:** ca. 35 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - Routen bekommen einen Fehler-Wrapper, `TicketRepository.find` fragt MongoDB direkt.

## Ausgangslage

- Lab 15.3 ist abgeschlossen, einschließlich der Vertiefung 14.4-14.7: Routen im Router, `async`, Repository auf MongoDB.

## Aufgaben

1. **Den Fehler reproduzieren.** Ruf `GET /tickets/gibts-nicht` auf. Was antwortet der Server, was steht im Log - und was passiert mit der **nächsten** Anfrage? (Lokal: `npm start`. Im Container: `docker compose logs backend` und `docker compose ps`.)
2. Erkläre in zwei Sätzen, warum die Fehler-Middleware aus Lab 14.5 hier nicht greift.
3. Schreib einen Wrapper `asyncHandler` in `src/http/async-handler.ts`, der abgelehnte Promises an die Fehler-Middleware weiterreicht, und leg ihn um alle Ticket-Routen.
4. Ersetze die Filterung im Speicher in `TicketRepository.find` durch eine MongoDB-Abfrage: Filter, Sortierung, Blättern und Gesamtzahl.
5. Lege zwei Tickets an, deren Titel mit einem Groß- und einem Kleinbuchstaben beginnen, und sortiere nach Titel. Passt die Reihenfolge? Wenn nicht: warum, und wie behebst du es?
6. Sorge dafür, dass die Datenbank weiß, dass `id` eindeutig ist.

## Checkpoint

- `GET /tickets/gibts-nicht` → `404`, `POST /tickets {}` → `422`, der Server läuft danach weiter.
- `?sort=title` sortiert "backup einrichten" zwischen "API dokumentieren" und "Containerize backend".
- Filter, `limit`, `offset` und `X-Total-Count` liefern dieselben Ergebnisse wie in Lab 14.7.

## Abschlusskriterien

- Keine Route ruft mehr `getAll()` auf, um danach im Speicher zu filtern.
- Du kannst erklären, warum Express 5 den Wrapper überflüssig machen würde.

## Fallback

Falls TypeScript beim Wrapper über `req.params` meckert (`string | string[]`): Die Typen von `@types/express` 5 sind auf Express 5 ausgelegt. Den Parametertyp im Wrapper ausdrücklich als `Record<string, string>` festlegen.
