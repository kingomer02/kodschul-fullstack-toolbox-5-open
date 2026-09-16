# Lab 12.3 - Lösung: Image-Größe und Layer-Caching

## Aufgabe 1: Größenvergleich

```bash
docker images | grep teamboard-backend
# teamboard-backend   multistage   <id>   ~180MB
# teamboard-backend   latest       <id>   ~220MB (Richtwert, enthält devDependencies)
```

## Aufgabe 2: `docker history`

```bash
docker history teamboard-backend:multistage
```

Die größte Schicht ist typischerweise `RUN npm ci --omit=dev` bzw. die `FROM node:20-alpine`-Basisschicht selbst.

## Aufgabe 3: Rebuild ohne Änderung

```bash
docker build -t teamboard-backend:multistage backend/
```

Alle Schichten zeigen `CACHED` - nichts hat sich geändert.

## Aufgabe 4: Nur Quellcode geändert

Nach einer Änderung an `backend/src/index.ts`: `COPY package.json package-lock.json ./` und `RUN npm ci` bleiben `CACHED`; `COPY . .` und alles danach wird neu ausgeführt.

## Aufgabe 5: `package.json` geändert

Nach einer Änderung an `backend/package.json`: bereits `COPY package.json package-lock.json ./` erkennt eine geänderte Datei, daher läuft auch `RUN npm ci` erneut.

## Grenzen

Die genannten Größen sind Richtwerte - Basis-Image-Updates von `node:20-alpine` können sie leicht verschieben; die relative Aussage (Multi-Stage kleiner als Single-Stage) bleibt bestehen.
