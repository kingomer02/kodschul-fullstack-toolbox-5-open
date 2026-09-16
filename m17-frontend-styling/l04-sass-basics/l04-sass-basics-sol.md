# Lab 17.4 - Lösung: Sass-Grundlagen für eigene Farben und Abstände

## Aufgabe 1-3: `main.scss`

Siehe vollständigen Code im Theorieteil (Lab 17.4, Abschnitt "Sass-Datei mit Variablen und Verschachtelung").

## Aufgabe 4: Klassen in `index.html`

```html
<!-- frontend/index.html (Ausschnitt) -->
<div class="col-12 col-md-4 column todo">
  <h2>To Do</h2>
  ...
</div>
<div class="col-12 col-md-4 column in-progress">
  <h2>In Progress</h2>
</div>
<div class="col-12 col-md-4 column done">
  <h2>Done</h2>
</div>
```

## Aufgabe 5: Ausblick auf Lab 17.5

Ein typischer Befehl zur Umwandlung wäre `sass frontend/styles/main.scss frontend/styles/main.css` - in Lab 17.5 übernimmt das ein Gulp-Task automatisch bei jeder Änderung.

## Grenzen

Ohne die Kompilierung aus Lab 17.5 versteht der Browser `.scss`-Dateien noch nicht direkt - `index.html` kann `main.scss` nicht als `<link>` einbinden.
