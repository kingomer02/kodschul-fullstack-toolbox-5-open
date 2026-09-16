# Lab 13.2 - Übung: `docker-compose.yml` für TeamBoard

**Dauer:** ca. 40 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - führt Backend und MongoDB erstmals gemeinsam per Compose aus.

## Ausgangslage

- `backend/Dockerfile` (Multi-Stage) aus Modul 12 liegt vor und baut erfolgreich.

## Aufgaben

1. Lege im Projekt-Root eine `docker-compose.yml` mit zwei Services an: `backend` (per `build: ./backend`) und `mongo` (Image `mongo:7`).
2. Ergänze bei `backend` eine Umgebungsvariable `MONGO_URL: mongodb://mongo:27017/teamboard` sowie `depends_on: [mongo]`.
3. Ergänze bei `mongo` ein benanntes Volume `mongo-data:/data/db` und deklariere `mongo-data` im `volumes:`-Abschnitt.
4. Starte alles im Hintergrund: `docker compose up -d`, prüfe mit `docker compose ps`, dass beide Services laufen.
5. Prüfe die Netzwerk-Erreichbarkeit von `mongo` aus dem `backend`-Container heraus (z. B. per `nslookup` oder `ping`, ggf. vorher passendes Tool im Container nachinstallieren).
6. Fahre alles wieder herunter: `docker compose down`. Committe `docker-compose.yml`.

## Checkpoint

- `docker compose ps` zeigt `backend` und `mongo` als `running`.
- Der `backend`-Container kann den Hostnamen `mongo` auflösen.

## Abschlusskriterien

- `docker-compose.yml` liegt im Projekt-Root und referenziert das bestehende Backend-Dockerfile, ohne dessen Inhalt zu verändern.

## Fallback

Falls `mongo:7` nicht startet (z. B. wegen zu wenig RAM in der Docker-Umgebung): versuchsweise `mongo:6` verwenden - das Verhalten für diese Übung (Erreichbarkeit, Volume) bleibt gleich.
