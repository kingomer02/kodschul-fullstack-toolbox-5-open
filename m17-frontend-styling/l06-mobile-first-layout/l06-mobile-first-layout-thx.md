# Modul 17: Frontend-Styling

## Lab 17.6 - Vertiefung: Mobile first, Layout ohne Breakpoints, Container Queries

---

## Lab-Ziel

In Lab 17.2 entscheidet **eine** Media Query bei 600px über das Layout, und sie schaut auf die Breite des **Bildschirms**. Du lernst drei modernere Werkzeuge kennen: mobile first denken, Spalten ohne festen Breakpoint umbrechen lassen und Komponenten nach **ihrem eigenen** Platz gestalten statt nach der Bildschirmbreite.

**Leitfragen:**

<details>
<summary>Was heißt "mobile first" konkret im CSS?</summary>

Die Grundregeln (ohne Media Query) beschreiben das **kleinste** Gerät. Größere Bildschirme bekommen Ergänzungen per `min-width`. Lab 17.2 macht es umgekehrt: Desktop als Grundlage, dann per `max-width` zurückbauen. Mobile first ist meist kürzer, weil einspaltige Layouts weniger Regeln brauchen - und es zwingt dazu, zuerst über das Wichtigste nachzudenken.

</details>

<details>
<summary>Warum reicht die Bildschirmbreite nicht, um eine Karte zu gestalten?</summary>

Dieselbe Ticketkarte steckt mal in einer breiten Spalte, mal in einer schmalen - bei **gleicher** Bildschirmbreite. Eine Media Query weiß nur, wie breit das Fenster ist, nicht, wie viel Platz die Karte hat. Container Queries fragen den umgebenden Container.

</details>

---

## Die vier Werkzeuge

**1 · Mobile first** - Grundregeln für schmal, Erweiterungen per `@media (min-width: ...)`.

**2 · Spalten ohne Media Query**

```css
grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
```

"So viele Spalten, wie hineinpassen, jede mindestens 16rem breit, der Rest wird verteilt." Der Umbruch passiert von selbst, dort wo er inhaltlich nötig ist.

`auto-fit` gegen `auto-fill`: Beide legen so viele Spuren an, wie hineinpassen. `auto-fit` **faltet leere Spuren auf 0px zusammen**, die belegten Spalten werden breiter. `auto-fill` lässt die leeren Spuren stehen.

**3 · Fließende Größen**

```css
font-size: clamp(1.5rem, 1rem + 2.5vw, 2.5rem);   /* minimal, bevorzugt, maximal */
```

**4 · Container Queries**

```css
.column { container-type: inline-size; }     /* dieses Element wird zum Container */

@container (min-width: 22rem) {             /* gilt, wenn der CONTAINER so breit ist */
  .ticket { ... }
}
```

---

## Brücke zu dem, was du kennst

Aus der Desktop-Welt (Swing, JavaFX) kennst du Layout-Manager, die nach dem verfügbaren Platz fragen, nicht nach der Bildschirmgröße. Container Queries bringen genau das ins CSS - erst seit 2023 in allen großen Browsern.

---

## Checkpoint

Bei 375px eine Spalte, bei 700px zwei, bei 1200px drei - ohne eine einzige Media Query für das Board. Die Ticketkarte ordnet sich nur in breiten Spalten zweispaltig an.

## Projektbezug

Freitag entsteht das Board in React mit Bootstrap. Dieselben Fragen (Wie viele Spalten? Wie sieht eine Karte in einer schmalen Spalte aus?) stellen sich dort wieder - dann kennst du die Werkzeuge unter Bootstraps Klassen.
