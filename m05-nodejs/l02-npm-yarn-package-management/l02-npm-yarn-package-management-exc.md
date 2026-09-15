# Lab 5.2 - Übung: NPM/Yarn-Paketmanagement

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - das TeamBoard-Backend-Projekt wird initialisiert.

## Ausgangslage

Das TeamBoard-Repo (Modul 3/4) enthält bisher Frontend-Dateien und eine minimale `package.json` mit Platzhalter-Skripten (Lab 4.2).

## Aufgaben

1. Lege im Repo einen Ordner `backend/` an und initialisiere darin ein eigenes Node-Projekt (`npm init -y`).
2. Installiere `express` als `dependency` und `typescript` sowie `@types/node` als `devDependencies`.
3. Ergänze eine `.gitignore` im Repo-Root um `node_modules/`, `dist/` und `.env`, falls noch nicht vorhanden.
4. Committe `package.json`, `package-lock.json` und `.gitignore` (nicht `node_modules/`).

## Checkpoint

- `backend/package.json` listet `express` unter `dependencies` und `typescript`/`@types/node` unter `devDependencies`.
- `git status` zeigt `node_modules/` nicht als neue Datei an.

## Abschlusskriterien

- `npm install` im `backend/`-Ordner läuft ohne Fehler durch.

## Fallback

Bei Netzwerkproblemen beim Installieren: einen vom Trainer bereitgestellten npm-Cache/Mirror nutzen oder die Pakete offline aus einem vorbereiteten Ordner kopieren.
