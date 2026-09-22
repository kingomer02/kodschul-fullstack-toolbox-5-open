# Lab 13.4 - Lösung: Healthchecks und Startreihenfolge

## Aufgabe 1-2: `docker-compose.yml`

```yaml
services:
  backend:
    build: ./backend
    ports:
      - "3000:3000"
    depends_on:
      mongo:
        condition: service_healthy
    environment:
      MONGO_URL: mongodb://mongo:27017/teamboard

  mongo:
    image: mongo:8
    volumes:
      - mongo-data:/data/db
    healthcheck:
      test: ["CMD", "mongosh", "--quiet", "--eval", "db.adminCommand('ping').ok"]
      interval: 5s
      timeout: 3s
      retries: 10
      start_period: 10s

volumes:
  mongo-data:
```

`db.adminCommand('ping')` ist der offizielle "Bist du da?"-Befehl von MongoDB. Antwortet der Server nicht, bricht `mongosh` mit einem Exit-Code ungleich 0 ab.

## Aufgabe 3: Startreihenfolge (gemessen 09/2026)

```text
 Container teamboard-mongo-1 Starting
 Container teamboard-mongo-1 Started
 Container teamboard-mongo-1 Waiting
 Container teamboard-mongo-1 Healthy
 Container teamboard-backend-1 Starting
 Container teamboard-backend-1 Started
```

```text
SERVICE   STATUS
backend   Up Less than a second
mongo     Up 6 seconds (healthy)
```

Das Backend startet erst etwa sechs Sekunden nach MongoDB - genau dann, wenn der erste Ping erfolgreich war.

## Aufgabe 4: Kaputter Healthcheck

Mit einem Test, der immer fehlschlägt (z. B. `--eval "quit(1)"`):

```text
 Container teamboard-mongo-1 Waiting
 Container teamboard-mongo-1 Error dependency mongo failed to start
dependency failed to start: container teamboard-mongo-1 is unhealthy
```

Das Backend wird **gar nicht erst gestartet**. Das ist gewollt: Lieber ein klarer Fehler beim Start als ein Backend, das halb läuft.

## Aufgabe 5: Commit

```bash
git add docker-compose.yml
git commit -m "feat: mongo healthcheck, backend wartet auf service_healthy"
```

## Grenzen

Der Healthcheck regelt nur den **Start**. Fällt MongoDB später aus, startet Compose das Backend nicht neu und hält es auch nicht an. Dafür gibt es `restart:`-Regeln oder einen Orchestrator wie Kubernetes.
