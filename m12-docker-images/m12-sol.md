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

Zeigt die Schichten beider Stages (Builder- und finale Stage), auch wenn im fertigen Image nur die finale Stage tatsächlich läuft.

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
