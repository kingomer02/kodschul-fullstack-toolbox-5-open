# Modul 12: Dockerfiles schreiben und optimieren

## Lab 12.2 - Build & Run mit Multi-Stage-Build

---

## Lab-Ziel

Du kannst das Backend-Dockerfile aus Modul 11 in einen Multi-Stage-Build umbauen, der nur die Laufzeit-Abhängigkeiten im finalen Image behält.

**Leitfragen:**

<details>
<summary>Was ist ein Multi-Stage-Build?</summary>

Ein Dockerfile mit mehreren `FROM`-Abschnitten ("Stages"), bei dem spätere Stages gezielt Dateien aus früheren Stages übernehmen (`COPY --from=...`), ohne deren übrige Inhalte (z. B. Build-Tools) zu übernehmen.

</details>

<details>
<summary>Warum will man `devDependencies` (z. B. TypeScript selbst) nicht im finalen Image haben?</summary>

Sie werden nur zum Kompilieren gebraucht, nicht zur Laufzeit - ihr Weglassen verkleinert das Image und reduziert die Angriffsfläche.

</details>

<details>
<summary>Was übernimmt die zweite Stage konkret vom Backend-Build?</summary>

Nur den kompilierten `dist/`-Ordner und die Produktions-`node_modules` - nicht den TypeScript-Quellcode oder die Build-Werkzeuge selbst.

</details>

---

## Vom Single-Stage- zum Multi-Stage-Build

Bisheriges Dockerfile (Modul 11): eine Stage, `npm ci` installiert auch `devDependencies` (inkl. `typescript`), die im finalen Image nicht mehr gebraucht werden.

```dockerfile
# backend/Dockerfile
FROM node:24-alpine AS builder
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:24-alpine
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci --omit=dev
COPY --from=builder /app/dist ./dist

CMD ["node", "dist/index.js"]
```

- **Stage `builder`:** installiert alle Abhängigkeiten (inkl. `typescript`) und kompiliert nach `dist/`.
- **Finale Stage:** installiert nur Produktionsabhängigkeiten (`--omit=dev`) und übernimmt ausschließlich `dist/` aus der `builder`-Stage.

---

## Bauen und prüfen

```bash
docker build -t teamboard-backend:multistage backend/
docker run --name teamboard-backend-ms teamboard-backend:multistage
docker logs teamboard-backend-ms
```

Die Ausgabe bleibt identisch zum Single-Stage-Build aus Modul 11 - nur der Bauprozess und das finale Image ändern sich.

---

## Checkpoint

Der Container aus `teamboard-backend:multistage` liefert dieselbe Ausgabe wie zuvor; `docker images` zeigt das neue Image neben dem alten Single-Stage-Stand.

Weiter geht es mit Lab 12.3: Image-Größe und Layer-Caching messen.
