# Transfer-Übung Modul 12 - Lösung: Backend-Image für die Weitergabe vorbereiten

## Aufgabe 1-2: Umtaggen und Aufräumen

```bash
docker tag teamboard-backend:multistage teamboard-backend:latest
docker images
docker rmi <alte-single-stage-image-id>
```

## Aufgabe 3: History prüfen

```bash
docker history teamboard-backend:latest
```

Zeigt **nur die Schichten der finalen Stage** (gemessen 09/2026, gekürzt):

```text
CMD ["node" "dist/index.js"]                    0B
COPY /app/dist ./dist # buildkit                81.9kB
RUN /bin/sh -c npm ci --omit=dev # buildkit     19.3MB
COPY package.json package-lock.json ./          49.2kB
WORKDIR /app                                    8.19kB
... darunter die Schichten von node:24-alpine
```

Der Beweis für Multi-Stage: `COPY /app/dist` holt das Ergebnis aus der Builder-Stage, aber `RUN npm run build` und das volle `npm ci` stehen **nicht** in der Liste. Die Builder-Stage existiert nur während des Builds und gehört nicht zum Image.

## Aufgabe 4: Abschlusstest

```bash
docker run --name teamboard-backend-final teamboard-backend:latest
docker logs teamboard-backend-final
# Vorher: To Do
# Nach 1. Aufruf: In Progress
# Nach 2. Aufruf: Done
```

## Grenzen

`docker tag` erstellt keinen neuen Image-Inhalt, sondern nur einen zusätzlichen Namen für dieselbe Image-ID - beide Tags zeigen bis zum expliziten Entfernen auf denselben Inhalt.
