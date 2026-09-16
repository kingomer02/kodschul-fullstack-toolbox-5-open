# Lab 12.3 - Übung: Image-Größe und Layer-Caching

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - reine Analyse des bestehenden Multi-Stage-Images aus Lab 12.2.

## Ausgangslage

- `teamboard-backend:multistage` aus Lab 12.2 ist gebaut; `teamboard-backend:latest` (Single-Stage, Modul 11) existiert noch lokal.

## Aufgaben

1. Vergleiche die Größe beider Tags mit `docker images | grep teamboard-backend`. Notiere den Unterschied.
2. Führe `docker history teamboard-backend:multistage` aus und identifiziere die größte Schicht.
3. Baue `teamboard-backend:multistage` ohne jede Codeänderung erneut und beobachte, welche Schritte `CACHED` zeigen.
4. Ändere nur `backend/src/index.ts` (z. B. einen Log-Text) und baue erneut - notiere, ab welcher Anweisung der Cache nicht mehr greift.
5. Ändere zusätzlich `backend/package.json` (z. B. eine Formatierungsänderung an einem bestehenden Feld reicht, wenn keine echte neue Abhängigkeit gewünscht ist) und baue erneut - beobachte, dass jetzt auch `npm ci` neu läuft.

## Checkpoint

- Der Größenunterschied zwischen Single-Stage- und Multi-Stage-Image ist anhand von `docker images` klar erkennbar.
- Nach einer reinen `index.ts`-Änderung bleibt die `npm ci`-Schicht im Build-Log als `CACHED` markiert.

## Abschlusskriterien

- Du kannst erklären, welche Dockerfile-Zeile bei welcher Art von Änderung den Cache für sich selbst und alle folgenden Schichten ungültig macht.

## Fallback

Falls kein Unterschied im Build-Log sichtbar ist: mit `docker build --progress=plain` bauen, um die Schicht-für-Schicht-Ausgabe ausführlicher anzuzeigen.
