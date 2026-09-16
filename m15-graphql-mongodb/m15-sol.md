# Transfer-Übung Modul 15 - Lösung: REST und GraphQL im Vergleich am selben Datensatz

## Aufgabe 1: Ticket anlegen (REST)

```bash
curl -X POST http://localhost:3000/tickets \
  -H "Content-Type: application/json" -d '{"title": "Vergleichsticket"}'
# 201 { "id": "t-1700000001111", "title": "Vergleichsticket", "status": "To Do", ... }
```

## Aufgabe 2: Abfrage per GraphQL (nur `title`)

```graphql
query {
  tickets {
    title
  }
}
```

```json
{ "data": { "tickets": [{ "title": "Vergleichsticket" }, ...] } }
```

## Aufgabe 3: Abfrage per REST

```bash
curl http://localhost:3000/tickets/t-1700000001111
# { "id": "t-1700000001111", "title": "Vergleichsticket", "description": "", "assignee": "", "status": "To Do" }
```

## Aufgabe 4: Beobachtung

Die REST-Antwort liefert immer alle Ticket-Felder, auch wenn nur der Titel gebraucht wird ("Over-Fetching"); die GraphQL-Antwort liefert exakt das angeforderte Feld `title` und keine überflüssigen Daten.

## Aufgabe 5: Persistenz nach Neustart

```bash
docker compose restart backend
curl http://localhost:3000/tickets/t-1700000001111
# weiterhin vorhanden

# GraphQL
query { tickets { id title } }
# enthält weiterhin "Vergleichsticket"
```

## Grenzen

Für einzelne, kleine Ressourcen wie ein Ticket ist der Unterschied im Datenvolumen gering - der Vorteil von GraphQL zeigt sich stärker bei verschachtelten oder sehr vielen Ressourcen gleichzeitig.
