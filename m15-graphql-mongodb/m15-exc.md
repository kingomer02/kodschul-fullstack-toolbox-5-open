# Transfer-Übung Modul 15 - Übung: REST und GraphQL im Vergleich am selben Datensatz

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - nutzt beide bereits bestehenden APIs nur über Anfragen.

## Ziel

Am selben, persistenten Ticket-Datensatz demonstrieren, dass REST (Modul 14) und GraphQL (Modul 15) auf derselben MongoDB-Datenbasis arbeiten - inklusive eines Blicks darauf, wie viel Daten jede Anfrageart überträgt.

## Ausgangslage

- Backend läuft containerisiert mit MongoDB-Anbindung und GraphQL unter `/graphql`.

## Aufgaben

1. Lege per `POST /tickets` (REST) ein neues Ticket an.
2. Frage dasselbe Ticket per GraphQL-`tickets`-Query ab, aber nur mit dem Feld `title` (ohne `id`, `status`, etc.).
3. Frage es zusätzlich per `GET /tickets/:id` (REST) ab und vergleiche die Antwortgröße/-felder mit der GraphQL-Antwort aus Schritt 2.
4. Halte in 2-3 Sätzen fest, welchen praktischen Vorteil die GraphQL-Antwort in Schritt 2 gegenüber der REST-Antwort in Schritt 3 hat.
5. Starte den Container neu (`docker compose restart backend`) und bestätige per REST **und** GraphQL, dass das Ticket weiterhin existiert.

## Checkpoint

- Die GraphQL-Antwort aus Schritt 2 enthält ausschließlich das angeforderte Feld `title`.
- Nach dem Neustart liefern sowohl `GET /tickets/:id` als auch die GraphQL-`tickets`-Query dasselbe Ticket.

## Abschlusskriterien

- Die Beobachtung aus Aufgabe 4 nennt konkret den Unterschied in der Feldauswahl (Over-/Under-Fetching), nicht nur eine allgemeine Präferenz.

## Lösungshinweise

```bash
curl -X POST http://localhost:3000/tickets \
  -H "Content-Type: application/json" -d '{"title": "Vergleichsticket"}'
```

```graphql
query {
  tickets {
    title
  }
}
```

```bash
curl http://localhost:3000/tickets/<id>
# liefert zusätzlich id, description, assignee, status - auch wenn nur der Titel interessiert
```

Vorteil GraphQL: die Antwort enthält exakt ein Feld statt aller Ticket-Felder - kein "Over-Fetching" ungenutzter Daten.

```bash
docker compose restart backend
curl http://localhost:3000/tickets/<id>
```

```graphql
query {
  tickets {
    id
    title
  }
}
```

## Fallback

Falls die Ticket-ID nach dem `POST` nicht mehr griffbereit ist: per GraphQL-`tickets`-Query (Feld `id` mit anfragen) erneut ermitteln.
