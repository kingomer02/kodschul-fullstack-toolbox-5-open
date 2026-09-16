# Transfer-Übung Modul 11 - Übung: Dockerfile aufräumen und wiederholbar machen

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - macht den Docker-Workflow aus den drei Labs alltagstauglich (Neubau nach Codeänderung, sauberes Aufräumen).

## Ziel

Die CLI-Grundlagen, den Image/Container-Unterschied und das erste Dockerfile aus Lab 11.1-11.3 so verbinden, dass ein Rebuild nach einer echten Codeänderung zur Routine wird.

## Ausgangslage

- `backend/Dockerfile` und `backend/.dockerignore` aus Lab 11.3 liegen vor; das Image `teamboard-backend` wurde einmal gebaut.

## Aufgaben

1. Ändere in `backend/src/index.ts` den Log-Text minimal (z. B. eine zusätzliche `console.log("Container build check")`-Zeile).
2. Baue das Image erneut mit einem Versions-Tag: `docker build -t teamboard-backend:v2 backend/`.
3. Starte einen neuen, benannten Container aus dem neuen Tag und prüfe per `docker logs`, dass die neue Zeile erscheint.
4. Liste mit `docker images` beide Tags (`teamboard-backend:latest` bzw. ohne Tag, `teamboard-backend:v2`) auf.
5. Räume konsequent auf: alten und neuen Container stoppen/entfernen, danach `docker image prune` (nur nicht mehr verwendete, ungetaggte Images) ausführen.

## Checkpoint

- Der Container aus `teamboard-backend:v2` zeigt die neue Log-Zeile, der alte Container/Image-Stand bleibt unverändert nachvollziehbar.
- `docker ps -a` ist nach dem Aufräumen leer (oder zeigt nur bewusst behaltene Container).

## Abschlusskriterien

- Du kannst nach einer Codeänderung eigenständig neu bauen, versionieren und aufräumen, ohne Anleitung Schritt für Schritt nachzulesen.

## Lösungshinweise

```bash
# Codeänderung in backend/src/index.ts vornehmen
docker build -t teamboard-backend:v2 backend/
docker run --name teamboard-backend-v2 teamboard-backend:v2
docker logs teamboard-backend-v2
docker images | grep teamboard-backend

docker stop teamboard-backend teamboard-backend-v2
docker rm teamboard-backend teamboard-backend-v2
docker image prune
```

## Fallback

Falls der Überblick über Container-Namen verloren geht: `docker ps -a --format "table {{.Names}}\t{{.Image}}\t{{.Status}}"` nutzen, um gezielt aufzuräumen statt zu raten.
