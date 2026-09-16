# Modul 17: Frontend-Styling

## Lab 17.2 - Responsives Design mit Grid und Flexbox

---

## Lab-Ziel

Du kannst mit CSS Grid eine mehrspaltige Seite bauen und mit Flexbox einzelne Elemente innerhalb einer Spalte anordnen, inklusive einem einfachen `@media`-Umbruch für kleine Bildschirme.

**Leitfragen:**

<details>
<summary>Wann verwendet man eher CSS Grid und wann eher Flexbox?</summary>

Grid eignet sich für zweidimensionale Layouts (Zeilen **und** Spalten gleichzeitig, z. B. mehrere Kanban-Spalten nebeneinander); Flexbox eignet sich für eindimensionale Anordnungen (z. B. Elemente innerhalb einer einzelnen Spalte untereinander).

</details>

<details>
<summary>Was bewirkt eine `@media (max-width: 600px)`-Regel?</summary>

Die darin enthaltenen CSS-Regeln gelten nur, wenn die Bildschirm- bzw. Viewport-Breite 600px oder weniger beträgt - typischerweise für mobile Geräte.

</details>

---

## Grid für die Spaltenanordnung

```css
/* sample-layout/styles.css */
.board {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}

@media (max-width: 600px) {
  .board {
    grid-template-columns: 1fr;
  }
}
```

## Flexbox für Elemente innerhalb einer Spalte

```css
.column {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}
```

## Beispiel-HTML

```html
<!-- sample-layout/index.html -->
<div class="board">
  <div class="column">
    <h2>To Do</h2>
    <div class="ticket">Ticket A</div>
    <div class="ticket">Ticket B</div>
  </div>
  <div class="column">
    <h2>In Progress</h2>
    <div class="ticket">Ticket C</div>
  </div>
  <div class="column">
    <h2>Done</h2>
  </div>
</div>
```

---

## Checkpoint

Bei einer Fensterbreite über 600px stehen die drei Spalten nebeneinander; unterhalb von 600px stehen sie untereinander - beobachtbar über die Entwicklertools des Browsers im responsiven Modus.

Weiter geht es mit Lab 17.3: Bootstrap 5 für die TeamBoard-Oberfläche.
