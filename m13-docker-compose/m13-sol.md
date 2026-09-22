# Transfer-Übung Modul 13 - Lösung: Day-3-Meilenstein bestätigen

## Aufgabe 1-4: Voller Zyklus

```bash
docker compose down -v
docker compose up -d --build
docker compose ps
# mongo     Up
# backend fehlt in der Liste: Exited (0), sichtbar mit docker compose ps -a
docker compose logs backend
# Vorher: To Do
# Nach 1. Aufruf: In Progress
# Nach 2. Aufruf: Done
docker compose run --rm --entrypoint sh backend -c "getent hosts mongo"
docker compose down
```

## Aufgabe 5: Was fehlt noch

Der MongoDB-Treiber ist noch nicht installiert, und `index.ts` liest `MONGO_URL` bisher nicht aus - beides kommt in Modul 15 hinzu, wenn Tickets tatsächlich in MongoDB gespeichert werden.

## Grenzen

Dieser Zyklus bestätigt nur Erreichbarkeit und CI-Validierung - eine echte Lese-/Schreib-Operation gegen MongoDB ist erst ab Modul 15 Teil des Projekts.
