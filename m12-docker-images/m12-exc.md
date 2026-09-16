# Transfer-Übung Modul 12 - Übung: Backend-Image für die Weitergabe vorbereiten

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - räumt alte Image-Stände auf und fixiert den Multi-Stage-Build als einzigen gültigen Stand.

## Ziel

Aus den drei Docker-Image-Labs einen sauberen, alleingültigen Backend-Image-Stand machen, statt mehrere parallele Tags (Single-Stage aus Modul 11, Multi-Stage aus Modul 12) nebeneinander zu behalten.

## Ausgangslage

- `teamboard-backend:latest` (Single-Stage) und `teamboard-backend:multistage` liegen beide lokal vor.

## Aufgaben

1. Tagge das Multi-Stage-Image als den neuen `latest`-Stand: `docker tag teamboard-backend:multistage teamboard-backend:latest`.
2. Entferne den alten Single-Stage-Image-Stand, sofern er unter einem eigenen Tag/ID noch existiert (`docker images`, dann gezielt `docker rmi <image-id>`).
3. Prüfe mit `docker history teamboard-backend:latest`, dass es sich jetzt tatsächlich um den Multi-Stage-Build handelt (Basis-Schichten erscheinen zweimal wegen der zwei Stages).
4. Starte final einen Container aus `teamboard-backend:latest` und bestätige die gewohnte Ausgabe.

## Checkpoint

- `docker images` zeigt für `teamboard-backend` nur noch einen relevanten, aktuellen Stand unter `latest`.
- Die Container-Ausgabe entspricht weiterhin dem bekannten Status-Übergang.

## Abschlusskriterien

- Es existiert kein veralteter Single-Stage-Image-Stand mehr, der versehentlich in Modul 13 (Docker Compose) verwendet werden könnte.

## Lösungshinweise

```bash
docker tag teamboard-backend:multistage teamboard-backend:latest
docker images
# alte, nicht mehr benötigte Image-ID gezielt entfernen:
docker rmi <alte-single-stage-image-id>
docker history teamboard-backend:latest
docker run --name teamboard-backend-final teamboard-backend:latest
docker logs teamboard-backend-final
```

## Fallback

Falls `docker rmi` mit "image is referenced in multiple repositories" abgelehnt wird: zuerst alle abhängigen Tags mit `docker rmi <tag>` einzeln entfernen, bevor die zugrunde liegende Image-ID gelöscht wird.
