# Modul 17: Frontend-Styling

## Lab 17.5 - Build-Automatisierung mit Gulp

---

## Lab-Ziel

Du richtest einen Gulp-Task ein, der `main.scss` automatisch zu `main.css` kompiliert, sobald sich die Datei ändert, und bindest das Ergebnis in `index.html` ein.

**Leitfragen:**

<details>
<summary>Warum reicht ein einmaliger Kompilierlauf oft nicht aus, sondern ein "Watch"-Modus ist praktischer?</summary>

Ohne Watch-Modus müsste nach jeder Änderung an `.scss` der Kompilierbefehl manuell erneut ausgeführt werden - ein Watch-Task erkennt Dateiänderungen automatisch und kompiliert sofort neu.

</details>

<details>
<summary>Was ist die Aufgabe von `gulp-sass` innerhalb der Gulp-Pipeline?</summary>

Es ist das Plugin, das den eigentlichen Sass-zu-CSS-Kompilierschritt innerhalb einer Gulp-Pipe (`.pipe(sass())`) übernimmt - Gulp selbst orchestriert nur den Ablauf.

</details>

---

## Gulp einrichten

```bash
cd frontend
npm init -y
npm install --save-dev gulp gulp-sass sass
```

```js
// frontend/gulpfile.js
const gulp = require("gulp");
const gulpSass = require("gulp-sass")(require("sass"));

function buildStyles() {
  return gulp
    .src("styles/main.scss")
    .pipe(gulpSass())
    .pipe(gulp.dest("styles"));
}

function watchStyles() {
  gulp.watch("styles/main.scss", buildStyles);
}

exports.build = buildStyles;
exports.watch = gulp.series(buildStyles, watchStyles);
```

```html
<!-- frontend/index.html (Ergänzung im <head>) -->
<link rel="stylesheet" href="styles/main.css" />
```

---

## Task ausführen

```bash
npx gulp build
# erzeugt frontend/styles/main.css aus main.scss

npx gulp watch
# kompiliert automatisch bei jeder Änderung an main.scss neu
```

---

## Checkpoint

Nach `npx gulp build` existiert `frontend/styles/main.css` mit den kompilierten Regeln aus Lab 17.4; im Browser zeigen sich die farbigen Spaltenrahmen und der Hover-Schatten auf den Ticket-Karten.

## Projektbezug

Damit ist das statische Grundgerüst für die Kanban-Oberfläche vollständig (HTML + Bootstrap + eigenes Sass, automatisiert kompiliert). Modul 18 baut daraus eine echte React-Komponentenstruktur.
