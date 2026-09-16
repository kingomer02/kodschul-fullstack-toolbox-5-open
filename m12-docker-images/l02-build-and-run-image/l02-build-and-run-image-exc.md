# Lab 12.2 - Übung: Build & Run mit Multi-Stage-Build

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - baut das Backend-Dockerfile aus Modul 11 zu einem Multi-Stage-Build um.

## Ausgangslage

- `backend/Dockerfile` (Single-Stage) aus Lab 11.3 liegt vor und baut/läuft erfolgreich.

## Aufgaben

1. Erweitere `backend/Dockerfile` um eine benannte Stage `builder` (`FROM node:20-alpine AS builder`), die wie bisher installiert und baut.
2. Ergänze eine zweite, finale Stage: neues `FROM node:20-alpine`, installiert nur Produktionsabhängigkeiten (`npm ci --omit=dev`) und übernimmt `dist/` per `COPY --from=builder /app/dist ./dist`.
3. Baue das Image neu unter einem neuen Tag: `docker build -t teamboard-backend:multistage backend/`.
4. Starte einen Container daraus und vergleiche die Log-Ausgabe mit dem Single-Stage-Container aus Modul 11.
5. Committe das aktualisierte `backend/Dockerfile`.

## Checkpoint

- Der Multi-Stage-Container liefert exakt dieselbe Ausgabe wie der Single-Stage-Container.
- `backend/Dockerfile` enthält jetzt zwei `FROM`-Anweisungen.

## Abschlusskriterien

- Das finale Image installiert keine `devDependencies` mehr (prüfbar in Lab 12.3 über die Image-Größe).

## Fallback

Falls `COPY --from=builder` einen Pfadfehler meldet: sicherstellen, dass der Stage-Name (`builder`) exakt in `FROM node:20-alpine AS builder` und in `COPY --from=builder` übereinstimmt.
