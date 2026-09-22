# Lab 17.6 - Lösung: Mobile first, Layout ohne Breakpoints, Container Queries

## HTML (Ausschnitt)

```html
<!-- sample-layout/index.html -->
<meta name="viewport" content="width=device-width, initial-scale=1" />
...
<main class="board">
  <section class="column">
    <h2>To Do</h2>
    <article class="ticket">
      <h3>Setup Repo</h3>
      <p>Initial repo structure and README</p>
      <span class="assignee">Alex</span>
      <button>Weiter →</button>
    </article>
    <!-- weitere Tickets -->
  </section>
  <section class="column"><h2>In Progress</h2> ... </section>
  <section class="column"><h2>Done</h2> ... </section>
</main>
```

Ohne `<meta name="viewport">` rendern Handys die Seite, als wäre sie 980px breit, und verkleinern sie dann - kein Layout greift wie gedacht.

## CSS

```css
/* sample-layout/styles.css */

/* 1 · Mobile first: die Grundregeln gelten für das kleinste Gerät */
body {
  margin: 0;
  padding: 1rem;
  font-family: system-ui, sans-serif;
}

h1 {
  font-size: clamp(1.5rem, 1rem + 2.5vw, 2.5rem); /* 3 · wächst stufenlos mit */
}

/* 2 · Spalten ohne Media Query: so viele wie hineinpassen, mindestens 16rem breit */
.board {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
  gap: 1rem;
}

.column {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  container-type: inline-size; /* 4 · die Spalte wird zum Container */
}

/* 4 · Karte schmal: alles untereinander */
.ticket {
  display: grid;
  gap: 0.25rem;
  padding: 0.75rem;
  border: 1px solid #ddd;
  border-radius: 8px;
}

.ticket h3,
.ticket p {
  margin: 0;
}

.ticket button {
  min-height: 44px; /* Fingergröße auf Touch-Geräten */
}

/* 4 · Karte breit: Titel und Text links, Zuständige und Button rechts */
@container (min-width: 22rem) {
  .ticket {
    grid-template-columns: 1fr auto;
    grid-template-areas:
      "title assignee"
      "text  action";
    align-items: center;
  }
  .ticket h3 { grid-area: title; }
  .ticket p { grid-area: text; }
  .ticket .assignee { grid-area: assignee; }
  .ticket button { grid-area: action; }
}
```

Für breite Bildschirme braucht es **keine einzige** zusätzliche Regel - `auto-fit` und die Container Query übernehmen alles.

## Aufgabe 6: Gemessen (Chrome, 09/2026)

| Fenster | Spuren des Boards | Spaltenbreite | Karte | Überschrift |
|---|---|---|---|---|
| 375px | `343px` | 343px | einspaltig (`317px`) | 25.4px |
| 700px | `326px 326px` | 326px, "Done" in Zeile 2 | einspaltig (`300px`) | 33.5px |
| 1200px | `378.7px 378.7px 378.7px 0px` | 379px | **zweispaltig** (`277px 71px`) | 40px |

**Warum die Karte bei 700px einspaltig bleibt:** Die Spalte ist 326px breit, die Container Query greift erst ab 22rem = 352px. Die Bildschirmbreite spielt keine Rolle.

**Die vierte Spur mit `0px` bei 1200px:** In 1168px (1200 minus Innenabstand) passen vier Spuren à 16rem. Drei sind belegt, `auto-fit` faltet die leere auf 0px zusammen.

## Aufgabe 7: `auto-fill` statt `auto-fit` (gemessen)

| Fenster | Spuren | Spaltenbreite | Karte |
|---|---|---|---|
| 1200px | `280px 280px 280px 280px` | 280px | **einspaltig** (`254px`) |

Mit `auto-fill` bleibt die leere vierte Spur stehen, die drei Spalten werden schmaler - und fallen damit unter 22rem. Die Karte wechselt zurück ins schmale Layout, **obwohl sich am Bildschirm nichts geändert hat.** Genau das ist der Punkt von Container Queries.

## Grenzen

`auto-fit` entscheidet nur nach der Breite. Soll "Done" auf dem Tablet bewusst neben "In Progress" stehen statt darunter, braucht es wieder eine explizite Regel. Die Werkzeuge ergänzen Media Queries, sie ersetzen sie nicht vollständig.
