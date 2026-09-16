# Transfer-Übung Modul 11 - Lösung: Dockerfile aufräumen und wiederholbar machen

## Aufgabe 1: Codeänderung

```ts
// backend/src/index.ts (Ausschnitt, ergänzt)
console.log("Container build check");
```

## Aufgabe 2-3: Neu bauen, versionieren, prüfen

```bash
docker build -t teamboard-backend:v2 backend/
docker run --name teamboard-backend-v2 teamboard-backend:v2
docker logs teamboard-backend-v2
# ... vorhandene Ausgabe ...
# Container build check
```

## Aufgabe 4: Beide Tags auflisten

```bash
docker images
# REPOSITORY          TAG      IMAGE ID   SIZE
# teamboard-backend    v2       <id>       ~180MB
# teamboard-backend    latest   <id>       ~180MB
```

## Aufgabe 5: Aufräumen

```bash
docker stop teamboard-backend teamboard-backend-v2
docker rm teamboard-backend teamboard-backend-v2
docker image prune
```

## Grenzen

`docker image prune` entfernt nur ungetaggte ("dangling") Images, keine benannten Tags wie `teamboard-backend:v2` - dafür wäre `docker rmi teamboard-backend:v2` nötig.
