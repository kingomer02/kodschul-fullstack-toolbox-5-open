# Lab 17.1 - Lösung: Schneller HTML schreiben mit Emmet

## Aufgabe 1: `#todo`-Spalte

Emmet-Eingabe: `div.column#todo>h2{To Do}+div.ticket*2>p{Ticket-Titel}`

```html
<div class="column" id="todo">
  <h2>To Do</h2>
  <div class="ticket">
    <p>Ticket-Titel</p>
  </div>
  <div class="ticket">
    <p>Ticket-Titel</p>
  </div>
</div>
```

## Aufgabe 2: `#in-progress`-Spalte

Emmet-Eingabe: `div.column#in-progress>h2{In Progress}+div.ticket>p{Ticket-Titel}`

```html
<div class="column" id="in-progress">
  <h2>In Progress</h2>
  <div class="ticket">
    <p>Ticket-Titel</p>
  </div>
</div>
```

## Aufgabe 3: Navigation

Emmet-Eingabe: `ul>li*5`

```html
<ul>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
</ul>
```

## Aufgabe 4: Zeitvergleich

Für dieselbe Struktur wären manuell deutlich mehr Tastenanschläge nötig gewesen (jedes öffnende und schließende Tag einzeln) - Emmet spart besonders bei sich wiederholenden, verschachtelten Strukturen Zeit.

## Grenzen

Emmet ersetzt kein Verständnis von HTML-Semantik - es beschleunigt nur das Tippen bereits geplanter Strukturen.
