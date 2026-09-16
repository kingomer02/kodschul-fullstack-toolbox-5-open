# Lab 14.1 - Übung: Ressourcen, HTTP-Methoden und Statuscodes

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - eigenständiges Beispielprojekt.

## Vorbereitung

- Ein leerer Ordner `sample-api/` mit `npm init -y` und `npm install express` sowie `npm install --save-dev typescript @types/express @types/node` liegt bereit.

## Aufgaben

1. Erstelle `sample-api/src/server.ts` mit einer `Item`-Ressource (`id`, `name`), einem In-Memory-Array und den Routen `GET /items` sowie `POST /items` (inkl. `400` bei fehlendem `name`).
2. Baue und starte den Server (`tsc` + `node`, oder `ts-node` falls installiert).
3. Teste mit `curl` (oder Postman): `GET /items` (leer), `POST /items` mit `{"name": "test"}` (Status `201`), erneutes `GET /items` (enthält das neue Element).
4. Teste den Fehlerfall: `POST /items` ohne `name` im Body - erwarte Status `400`.

## Checkpoint

- `POST /items` mit gültigem Body liefert Status `201` und das erstellte Element.
- `POST /items` ohne `name` liefert Status `400`.

## Abschlusskriterien

- Alle vier Anfragen liefern die in der Theorie beschriebenen Statuscodes.

## Fallback

Falls `curl` nicht verfügbar ist: Postman oder die VS-Code-Erweiterung "REST Client" mit einer `.http`-Datei nutzen.
