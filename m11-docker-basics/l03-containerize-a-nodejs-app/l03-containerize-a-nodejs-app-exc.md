# Lab 11.3 - Übung: Eine Node.js-App containerisieren

**Dauer:** ca. 40 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - erstes Dockerfile für das Backend.

## Ausgangslage

- `backend/` enthält den TypeScript-Stand aus der Modul-8-Transfer-Übung (Repository, Service, Beispieltickets, `npm run build`/`npm start` funktionieren lokal).

## Aufgaben

1. Lege `backend/Dockerfile` an, das: Node 24 (Alpine) als Basis nutzt, zuerst `package.json`/`package-lock.json` kopiert und `npm ci` ausführt, dann den restlichen Code kopiert, mit `npm run build` baut und per `CMD` `node dist/index.js` startet.
2. Lege `backend/.dockerignore` mit `node_modules`, `dist` und `.git` an.
3. Baue das Image: `docker build -t teamboard-backend backend/` (Build-Kontext ist der `backend/`-Ordner).
4. Starte einen Container daraus und prüfe die Logs.
5. Committe `backend/Dockerfile` und `backend/.dockerignore`.

## Checkpoint

- `docker images` listet `teamboard-backend`.
- `docker logs teamboard-backend` zeigt dieselbe Ausgabe wie der lokale `npm start`-Lauf (Status-Übergänge To Do -> In Progress -> Done).

## Abschlusskriterien

- Das Backend läuft containerisiert, ohne dass am TypeScript-Code selbst etwas geändert wurde.

## Fallback

Falls der Build mit einem Fehler zu `npm ci` abbricht: prüfen, ob `package-lock.json` tatsächlich committet und im Build-Kontext (`backend/`) vorhanden ist - `npm ci` schlägt ohne Lock-File fehl.
