# Lab 14.3 - Lösung: Die API im Container testen

## Aufgabe 1: Portfreigabe

```yaml
# docker-compose.yml (Ausschnitt)
services:
  backend:
    build: ./backend
    ports:
      - "3000:3000"
    depends_on:
      - mongo
    environment:
      MONGO_URL: mongodb://mongo:27017/teamboard
```

## Aufgabe 2-5: Bauen, starten, testen

```bash
docker compose up -d --build
docker compose ps
# backend   running
# mongo     running

curl http://localhost:3000/tickets
# [{ "id": "t-1", ... }, ...]

docker compose logs backend
# TeamBoard backend listening on port 3000
```

## Aufgabe 6: Commit

```bash
git add docker-compose.yml
git commit -m "feat: expose backend port in docker-compose.yml"
```

## Grenzen

Ohne die `ports`-Zuordnung wäre der Server im Container zwar aktiv gewesen, aber `curl http://localhost:3000` hätte "Connection refused" gemeldet - der Container selbst lief bereits vorher korrekt.
