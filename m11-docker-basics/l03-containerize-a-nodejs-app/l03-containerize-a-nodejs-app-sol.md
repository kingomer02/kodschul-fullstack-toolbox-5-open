# Lab 11.3 - Lösung: Eine Node.js-App containerisieren

## Aufgabe 1: Dockerfile

```dockerfile
# backend/Dockerfile
FROM node:24-alpine

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci

COPY . .
RUN npm run build

CMD ["node", "dist/index.js"]
```

## Aufgabe 2: `.dockerignore`

```text
node_modules
dist
.git
```

## Aufgabe 3-4: Bauen und starten

```bash
docker build -t teamboard-backend backend/
docker run --name teamboard-backend teamboard-backend
docker logs teamboard-backend
```

Erwartete Ausgabe:

```text
Vorher: To Do
Nach 1. Aufruf: In Progress
Nach 2. Aufruf: Done
```

## Aufgabe 5: Commit

```bash
git add backend/Dockerfile backend/.dockerignore
git commit -m "feat: add Dockerfile for backend"
```

## Grenzen

Der Container beendet sich nach Ausgabe der Logs von selbst, da `index.ts` (noch) kein dauerhaft laufender Server ist - das ändert sich erst mit der REST-API in Modul 14.
