# Lab 16.2 - Lösung: Login-Flow für TeamBoard implementieren

## Aufgabe 1: Installation

```bash
cd backend
npm install bcrypt jsonwebtoken
npm install --save-dev @types/bcrypt @types/jsonwebtoken
```

## Aufgabe 2-5: Auth-Dateien

Siehe vollständigen Code im Theorieteil (Lab 16.2, Abschnitte "Nutzerverwaltung und Login-Routen" und "Middleware für geschützte Routen").

## Aufgabe 6: `docker-compose.yml`

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
      JWT_SECRET: local-dev-secret-change-me
```

## Aufgabe 7: Testen

```bash
curl -X POST http://localhost:3000/auth/register \
  -H "Content-Type: application/json" -d '{"username": "alex", "password": "hunter2"}'
# 201 { "username": "alex" }

curl -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" -d '{"username": "alex", "password": "hunter2"}'
# 200 { "token": "eyJhbGciOi..." }

curl -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" -d '{"username": "alex", "password": "falsch"}'
# 401 { "error": "invalid credentials" }
```

## Grenzen

Nutzer liegen weiterhin nur im Arbeitsspeicher - ein Backend-Neustart löscht alle registrierten Konten (eine Mongo-Collection für Nutzer wäre eine reale Erweiterung, aber nicht Teil dieses Kurses).
