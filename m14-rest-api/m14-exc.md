# Transfer-Übung Modul 14 - Übung: Vollständigen Ticket-Lebenszyklus über die API abbilden

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - nutzt die bestehende API rein über Anfragen, ändert keinen Code.

## Ziel

Alle drei REST-Labs (Statuscodes, Ticket-Endpunkte, Container-Test) zu einem einzigen End-to-End-Szenario verbinden: ein Ticket komplett von der Erstellung bis "Done" begleiten - ausschließlich über HTTP-Anfragen gegen den laufenden Container.

## Ausgangslage

- `docker compose up -d --build` läuft, `backend` ist unter `http://localhost:3000` erreichbar.

## Aufgaben

1. Lege per `POST /tickets` ein neues Ticket an (`title`, `description`, `assignee`).
2. Weise es per `PATCH /tickets/:id/assign` einer anderen Person zu.
3. Bewege es zweimal per `PATCH /tickets/:id/status` weiter, bis es `Done` ist.
4. Prüfe nach jedem Schritt per `GET /tickets/:id`, dass der erwartete Zustand tatsächlich gespeichert wurde.
5. Versuche abschließend, ein nicht existierendes Ticket zuzuweisen (`PATCH /tickets/unbekannte-id/assign`) und bestätige den `404`-Fehlerfall.

## Checkpoint

- Nach Schritt 3 zeigt `GET /tickets/:id` den Status `Done` und die in Schritt 2 gesetzte `assignee`.
- Schritt 5 liefert zuverlässig `404`.

## Abschlusskriterien

- Der komplette Ticket-Lebenszyklus (anlegen → zuweisen → zweimal Status ändern) wurde ausschließlich über die REST-API demonstriert, ohne Code zu ändern.

## Lösungshinweise

```bash
curl -X POST http://localhost:3000/tickets \
  -H "Content-Type: application/json" \
  -d '{"title": "Neues Feature", "description": "Testen", "assignee": "Alex"}'
# -> id, z.B. "t-1700000000000"

curl -X PATCH http://localhost:3000/tickets/<id>/assign \
  -H "Content-Type: application/json" -d '{"assignee": "Sam"}'

curl -X PATCH http://localhost:3000/tickets/<id>/status
curl -X PATCH http://localhost:3000/tickets/<id>/status
curl http://localhost:3000/tickets/<id>
# status: "Done", assignee: "Sam"

curl http://localhost:3000/tickets/unbekannte-id/assign -X PATCH \
  -H "Content-Type: application/json" -d '{"assignee": "Sam"}'
# 404
```

## Fallback

Falls die ID aus der `POST`-Antwort nicht mehr griffbereit ist: `GET /tickets` liefert alle Tickets erneut, inklusive der zuletzt erzeugten ID.
