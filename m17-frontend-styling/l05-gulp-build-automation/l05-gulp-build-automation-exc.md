# Lab 17.5 - Übung: Build-Automatisierung mit Gulp

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - richtet die Gulp-Pipeline ein, die `main.scss` in ausgeliefertes CSS umwandelt.

## Ausgangslage

- `frontend/styles/main.scss` (Lab 17.4) liegt vor; `frontend/index.html` bindet noch keine kompilierte CSS-Datei ein.

## Aufgaben

1. Führe `npm init -y` im `frontend/`-Ordner aus und installiere `gulp`, `gulp-sass`, `sass` als Dev-Abhängigkeiten.
2. Erstelle `frontend/gulpfile.js` mit einem `build`-Task (kompiliert `styles/main.scss` nach `styles/`) und einem `watch`-Task.
3. Führe `npx gulp build` aus und prüfe, dass `frontend/styles/main.css` entsteht.
4. Ergänze in `index.html` ein `<link rel="stylesheet" href="styles/main.css">` und öffne die Datei im Browser - prüfe die farbigen Spaltenrahmen aus Lab 17.4.
5. Starte `npx gulp watch`, ändere eine Farbe in `main.scss` und beobachte, dass `main.css` automatisch neu erzeugt wird.
6. Committe `gulpfile.js`, `package.json` und die aktualisierte `index.html` (die generierte `main.css` kann optional per `.gitignore` ausgeschlossen werden).

## Checkpoint

- `npx gulp build` erzeugt `main.css` fehlerfrei.
- Nach einer Änderung an `main.scss` im Watch-Modus aktualisiert sich `main.css` automatisch, ohne erneuten manuellen Befehl.

## Abschlusskriterien

- Der Browser zeigt die in Lab 17.4 definierten Farben und den Hover-Effekt tatsächlich an, nicht nur unkompiliertes Sass.

## Fallback

Falls `gulp-sass` Versionskonflikte mit der `sass`-Bibliothek verursacht: Versionsangaben aus der offiziellen `gulp-sass`-Dokumentation exakt übernehmen, da beide Pakete kompatible Versionen benötigen.
