# Lab 18.3 - Übung: React-Projekt-Setup für TeamBoard

**Dauer:** ca. 45 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - ersetzt den statischen `frontend/`-Stand aus Modul 17 durch ein echtes Vite-React-TS-Projekt.

## Ausgangslage

- `frontend/index.html`, `frontend/styles/main.scss` (Modul 17) liegen vor.

## Aufgaben

1. Sichere `frontend/styles/main.scss` (z. B. per Kopie), da der Ordner gleich neu aufgesetzt wird.
2. Richte im `frontend/`-Ordner ein neues Vite-React-TS-Projekt ein (`npm create vite@latest frontend -- --template react-ts` - ggf. bestehenden Ordnerinhalt vorher sichern/löschen) und installiere die Abhängigkeiten sowie `bootstrap`.
3. Kopiere `main.scss` nach `frontend/src/styles/main.scss` und importiere sowohl Bootstrap-CSS als auch `main.scss` in `frontend/src/main.tsx`.
4. Übertrage `TicketCard` und `Column` aus Lab 18.2 nach `frontend/src/components/`.
5. Erstelle `frontend/src/data/sample-tickets.ts` mit Beispieldaten für alle drei Spalten.
6. Baue `App.tsx` so um, dass alle drei Spalten mit den passenden CSS-Klassen (`column todo`, `column in-progress`, `column done`) aus Modul 17 gerendert werden.
7. Starte `npm run dev` und prüfe, dass Farben, Rahmen und Kartenlayout aus Modul 17 weiterhin sichtbar sind.
8. Committe den neuen `frontend/`-Ordner (inkl. Entfernen der alten `gulpfile.js`/`index.html`, falls durch das neue Setup ersetzt).

## Checkpoint

- Das Board zeigt drei farbig umrandete Spalten mit den in Lab 18.2 gebauten `TicketCard`-Komponenten.

## Abschlusskriterien

- Es existiert kein Gulp-Build mehr im `frontend/`-Ordner - Vite übernimmt die Sass-Kompilierung direkt beim Start.

## Fallback

Falls Vite beim Einrichten in einem nicht-leeren Ordner abbricht: den vorhandenen `frontend/`-Inhalt vorübergehend in einen Ordner `frontend-static-backup/` verschieben, dann Vite im leeren `frontend/` einrichten.
