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
    image: mongo:7
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

## Aufgabe 4: Starten und prüfen

```bash
docker compose up -d
docker compose ps
# NAME               STATUS
# teamboard-backend-1   running
# teamboard-mongo-1     running
```

## Aufgabe 5: Erreichbarkeit prüfen

```bash
docker compose exec backend sh -c "apk add --no-cache bind-tools && nslookup mongo"
# Name: mongo
# Address: 172.x.x.x
```

## Aufgabe 6: Herunterfahren und Commit

```bash
docker compose down
git add docker-compose.yml
git commit -m "feat: add docker-compose.yml for backend and mongo"
```

## Grenzen

Das Backend liest `MONGO_URL` noch nicht - die Variable ist vorbereitet, aber ungenutzt, bis Modul 15 den MongoDB-Treiber tatsächlich einbindet.
