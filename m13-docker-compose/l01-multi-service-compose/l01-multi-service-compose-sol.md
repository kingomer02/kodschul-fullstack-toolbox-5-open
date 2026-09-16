# Lab 13.1 - Lösung: Mehrere Services verbinden

## Aufgabe 1-2: `docker-compose.yml`

```yaml
# sample-compose/docker-compose.yml
services:
  cache:
    image: redis:7-alpine
  app:
    image: alpine
    command: sh -c "apk add --no-cache redis && redis-cli -h cache ping"
    depends_on:
      - cache
```

## Aufgabe 3-4: Starten und beenden

```bash
docker compose -f sample-compose/docker-compose.yml up
# app-1    | PONG
```

```bash
docker compose -f sample-compose/docker-compose.yml down
```

## Grenzen

`depends_on` wartet nur, bis der Container von `cache` gestartet wurde, nicht darauf, dass Redis intern bereits Verbindungen annimmt - bei zeitkritischen Fällen sind zusätzliche Healthchecks nötig (nicht Teil dieser Übung).
