# Transfer-Übung Modul 5 - Übung: Lauffähiges Backend-Platzhalterskript

**Dauer:** ca. 15 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - macht das in Lab 5.1/5.2 initialisierte Backend erstmals ausführbar.

## Ziel

Aus einem nur initialisierten `backend/`-Ordner (Pakete installiert, aber nichts läuft) ein tatsächlich ausführbares Mini-Skript machen - der Unterschied zwischen "Projekt existiert" und "Projekt läuft".

## Ausgangslage

- `backend/package.json` mit `express` als Abhängigkeit und `typescript`/`@types/node` als Dev-Abhängigkeit aus Lab 5.2.

## Aufgaben

1. Lege `backend/src/index.js` an mit `console.log("TeamBoard backend placeholder");`.
2. Ergänze in `backend/package.json` ein Skript: `"start": "node src/index.js"`.
3. Führe `npm start` im `backend/`-Ordner aus und prüfe die Konsolenausgabe.
4. Committe `backend/package.json`, `backend/src/index.js` gemeinsam mit einer aussagekräftigen Nachricht.

## Checkpoint

- `npm start` in `backend/` gibt exakt `TeamBoard backend placeholder` aus, ohne Fehler.

## Abschlusskriterien

- Der Backend-Ordner enthält ein lauffähiges, wenn auch minimales Skript - bereit für die Umstellung auf TypeScript in Modul 6.

## Fallback

Falls `npm start` mit "Cannot find module" fehlschlägt: Pfad in `src/index.js` und Arbeitsverzeichnis (`backend/`) prüfen - ein häufiger Fehler ist, den Befehl aus dem Projekt-Root statt aus `backend/` auszuführen.
