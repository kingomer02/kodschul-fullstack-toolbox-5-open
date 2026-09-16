# Lab 12.2 - Lösung: Build & Run mit Multi-Stage-Build

## Aufgabe 1-2: Multi-Stage-Dockerfile

```dockerfile
# backend/Dockerfile
FROM node:20-alpine AS builder
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:20-alpine
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci --omit=dev
COPY --from=builder /app/dist ./dist

CMD ["node", "dist/index.js"]
```

## Aufgabe 3-4: Bauen und vergleichen

```bash
docker build -t teamboard-backend:multistage backend/
docker run --name teamboard-backend-ms teamboard-backend:multistage
docker logs teamboard-backend-ms
```

Ausgabe ist identisch zum Single-Stage-Container aus Modul 11.

## Aufgabe 5: Commit

```bash
git add backend/Dockerfile
git commit -m "refactor: convert backend Dockerfile to multi-stage build"
```

## Grenzen

Der Build dauert durch zwei `npm ci`-Läufe (Builder- und finale Stage) tendenziell etwas länger als der Single-Stage-Build - das finale Image ist dafür kleiner (siehe Lab 12.3).
