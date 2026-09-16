# Lab 14.3 - Übung: Die API im Container testen

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - ergänzt die Portfreigabe in `docker-compose.yml`, damit die API vom Host aus erreichbar ist.

## Ausgangslage

- `backend/src/index.ts` läuft als Express-Server (Lab 14.2); `docker-compose.yml` (Modul 13) hat noch keine Portfreigabe.

## Aufgaben

1. Ergänze in `docker-compose.yml` beim `backend`-Service `ports: ["3000:3000"]`.
2. Baue und starte alles neu: `docker compose up -d --build`.
3. Prüfe mit `docker compose ps`, dass `backend` dauerhaft `running` bleibt (nicht `exited`).
4. Teste mit `curl http://localhost:3000/tickets` vom Host aus.
5. Prüfe mit `docker compose logs backend`, dass die Startmeldung erscheint.
6. Committe die aktualisierte `docker-compose.yml`.

## Checkpoint

- `docker compose ps` zeigt `backend` als `running`, nicht `exited`.
- `curl http://localhost:3000/tickets` liefert vom Host aus die Ticketliste.

## Abschlusskriterien

- Die REST-API ist vollständig containerisiert nutzbar, ohne dass sich der Anwendungscode gegenüber Lab 14.2 ändert.

## Fallback

Falls Port 3000 auf dem Host bereits belegt ist: `ports: ["3001:3000"]` verwenden und entsprechend `http://localhost:3001` testen.
