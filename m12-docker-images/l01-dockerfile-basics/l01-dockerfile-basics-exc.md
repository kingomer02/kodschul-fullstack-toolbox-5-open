# Lab 12.1 - Übung: Dockerfile-Grundlagen

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - eigenständiges Beispielprojekt.

## Vorbereitung

- Ein leerer Ordner `sample-app/` liegt lokal bereit.

## Aufgaben

1. Lege `sample-app/greet.js` an: liest `process.env.GREET_NAME` (Fallback `"world"`) und loggt `Hello, <name>!`.
2. Schreibe `sample-app/Dockerfile`: Basis `node:20-alpine`, `WORKDIR /app`, kopiert `greet.js`, setzt `ENV GREET_NAME=Docker`, startet per `CMD` das Skript.
3. Baue das Image: `docker build -t greet-sample sample-app/`.
4. Starte es einmal ohne und einmal mit überschriebener Umgebungsvariable (`docker run -e GREET_NAME=Kurs greet-sample`).

## Checkpoint

- `docker run greet-sample` gibt `Hello, Docker!` aus.
- `docker run -e GREET_NAME=Kurs greet-sample` gibt `Hello, Kurs!` aus.

## Abschlusskriterien

- Ein eigenständiges Dockerfile für eine Node-Anwendung wurde ohne Vorlage geschrieben und läuft.

## Fallback

Falls `docker build` mit "file not found" fehlschlägt: prüfen, dass `greet.js` im selben Ordner wie das `Dockerfile` liegt und der Build-Kontext (`sample-app/`) korrekt angegeben ist.
