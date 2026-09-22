# Lab 13.2 - Lösung: `docker-compose.yml` für TeamBoard

## Aufgabe 1-3: `docker-compose.yml`

```yaml
# docker-compose.yml
services:
  backend:
    build: ./backend
    depends_on:
      - mongo
    environment:
      MONGO_URL: mongodb://mongo:27017/teamboard

  mongo:
    image: mongo:8
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

## Aufgabe 4: Starten und prüfen

```bash
docker compose up -d
docker compose ps
# NAME                IMAGE     STATUS
# teamboard-mongo-1   mongo:8   Up 8 seconds

docker compose ps -a
# backend: Exited (0) - das Skript ist durchgelaufen, kein Absturz
```

## Aufgabe 5: Erreichbarkeit prüfen

```bash
docker compose run --rm --entrypoint sh backend -c "getent hosts mongo"
# 172.22.0.2   mongo  mongo
```

`exec` funktioniert hier nicht: Es braucht einen **laufenden** Container, `backend` ist aber schon beendet (`Exited (0)`). `run` startet dafür einen frischen Container aus demselben Service - im selben Netzwerk. `getent` ist im Alpine-Image bereits enthalten, es muss nichts nachinstalliert werden.

## Aufgabe 6: Herunterfahren und Commit

```bash
docker compose down
git add docker-compose.yml
git commit -m "feat: add docker-compose.yml for backend and mongo"
```

## Grenzen

Das Backend liest `MONGO_URL` noch nicht - die Variable ist vorbereitet, aber ungenutzt, bis Modul 15 den MongoDB-Treiber tatsächlich einbindet.
