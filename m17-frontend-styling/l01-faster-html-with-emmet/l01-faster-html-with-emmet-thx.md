# Modul 17: Frontend-Styling

## Lab 17.1 - Schneller HTML schreiben mit Emmet

---

## Lab-Ziel

Du kannst mit Emmet-Kürzeln in VS Code deutlich schneller HTML-Grundgerüste erzeugen als durch manuelles Tippen.

**Leitfragen:**

<details>
<summary>Was macht Emmet aus `div.card>h2+p` beim Drücken von Tab?</summary>

Es erzeugt ein `<div class="card">` mit einem `<h2>` gefolgt von einem `<p>` als direkte Kindelemente - `>` steht für "Kind", `+` für "Geschwister".

</details>

<details>
<summary>Wie erzeugt man mit Emmet drei gleichartige `<li>`-Elemente auf einmal?</summary>

Mit der Multiplikation `li*3` gefolgt von Tab.

</details>

---

## Emmet-Kürzel im Überblick

| Kürzel          | Ergebnis                                                  |
| --------------- | --------------------------------------------------------- |
| `div.card`      | `<div class="card"></div>`                                |
| `ul>li*3`       | `<ul>` mit drei `<li>`-Kindern                            |
| `div.card>h2+p` | `<div class="card">` mit `<h2>` und `<p>` als Geschwister |
| `.column#todo`  | `<div class="column" id="todo"></div>`                    |

## Beispiel: Kanban-Spalte per Emmet

Eingabe: `div.column#todo>h2{To Do}+div.ticket*2>p{Ticket-Titel}`

Ergebnis nach Tab:

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

---

## Checkpoint

Du erzeugst mit einem einzigen Emmet-Kürzel ein `div.column` mit einer Überschrift und zwei `div.ticket`-Kindelementen, ohne die schließenden Tags manuell zu tippen.

Weiter geht es mit Lab 17.2: responsives Design mit Grid und Flexbox.
