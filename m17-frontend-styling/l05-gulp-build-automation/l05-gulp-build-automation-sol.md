# Lab 17.5 - Lösung: Build-Automatisierung mit Gulp

## Aufgabe 1: Installation

```bash
cd frontend
npm init -y
npm install --save-dev gulp gulp-sass sass
```

## Aufgabe 2: `gulpfile.js`

Siehe vollständigen Code im Theorieteil (Lab 17.5, Abschnitt "Gulp einrichten").

## Aufgabe 3: Build ausführen

```bash
npx gulp build
# frontend/styles/main.css wurde erzeugt
```

## Aufgabe 4: Einbinden und prüfen

```html
<!-- frontend/index.html (Ausschnitt im <head>) -->
<link
  href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
  rel="stylesheet"
/>
<link rel="stylesheet" href="styles/main.css" />
```

Im Browser: farbige obere Ränder je Spalte, abgerundete Ticket-Karten mit Hover-Schatten.

## Aufgabe 5: Watch-Modus testen

```bash
npx gulp watch
# Farbe in main.scss ändern -> main.css wird automatisch neu erzeugt
```

## Aufgabe 6: Commit

```bash
echo "styles/main.css" >> .gitignore
git add gulpfile.js package.json package-lock.json index.html styles/main.scss .gitignore
git commit -m "feat: add Gulp pipeline to compile Sass to CSS"
```

## Grenzen

Der Watch-Modus läuft nur, solange das Terminal-Fenster aktiv bleibt - für eine dauerhafte Automatisierung wäre ein CI-Build-Schritt (ähnlich Modul 4) eine sinnvolle, hier aber nicht umgesetzte Erweiterung.
