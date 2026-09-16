# Lab 17.2 - Lösung: Responsives Design mit Grid und Flexbox

## Aufgabe 1: HTML

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

## Aufgabe 2-4: CSS

```css
/* sample-layout/styles.css */
.board {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}

.column {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

@media (max-width: 600px) {
  .board {
    grid-template-columns: 1fr;
  }
}
```

## Aufgabe 5: Testen

Im responsiven Modus der Entwicklertools bei einer simulierten Breite von z. B. 375px stehen die drei Spalten untereinander; ab 601px stehen sie nebeneinander.

## Grenzen

Dieses Beispiel nutzt nur einen einzigen Breakpoint (600px) - ein reales responsives Layout hätte oft mehrere Zwischenstufen (z. B. Tablet-Breite mit zwei Spalten).
