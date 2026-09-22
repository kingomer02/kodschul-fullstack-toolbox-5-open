# Lab 13.2 - Übung: `docker-compose.yml` für TeamBoard

**Dauer:** ca. 40 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - führt Backend und MongoDB erstmals gemeinsam per Compose aus.

## Ausgangslage

- `backend/Dockerfile` (Multi-Stage) aus Modul 12 liegt vor und baut erfolgreich.

## Aufgaben

1. Lege im Projekt-Root eine `docker-compose.yml` mit zwei Services an: `backend` (per `build: ./backend`) und `mongo` (Image `mongo:8`).
2. Ergänze bei `backend` eine Umgebungsvariable `MONGO_URL: mongodb://mongo:27017/teamboard` sowie `depends_on: [mongo]`.
3. Ergänze bei `mongo` ein benanntes Volume `mongo-data:/data/db` und deklariere `mongo-data` im `volumes:`-Abschnitt.
4. Starte alles im Hintergrund: `docker compose up -d`, prüfe mit `docker compose ps`, dass beide Services laufen.
5. Prüfe die Namensauflösung von `mongo` aus einem `backend`-Container heraus.

> **Hinweis:** `docker compose exec` setzt einen laufenden Container voraus - `backend` ist aber schon wieder beendet. Überlegt, welcher Compose-Befehl stattdessen einen neuen Container desselben Service startet.
6. Fahre alles wieder herunter: `docker compose down`. Committe `docker-compose.yml`.

## Checkpoint

- `docker compose ps` zeigt `mongo` als `running`; `backend` läuft einmal durch und endet mit `Exited (0)`.

> **Warum `backend` nicht dauerhaft läuft:** `index.ts` ist ein Skript, kein Server - der Container startet, führt es aus und beendet sich ordentlich mit Code 0. Ein dauerhaft laufender Service entsteht erst in Modul 14 mit Express.
- Der `backend`-Container kann den Hostnamen `mongo` auflösen.

## Abschlusskriterien

- `docker-compose.yml` liegt im Projekt-Root und referenziert das bestehende Backend-Dockerfile, ohne dessen Inhalt zu verändern.

## Fallback

Falls `mongo:8` nicht startet (z. B. wegen zu wenig RAM in der Docker-Umgebung): der Docker-Umgebung mehr Arbeitsspeicher zuweisen (Docker Desktop → Settings → Resources) oder versuchsweise `mongo:7` verwenden - das Verhalten für diese Übung (Erreichbarkeit, Volume) bleibt gleich.
