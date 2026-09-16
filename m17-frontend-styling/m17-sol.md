# Transfer-Übung Modul 17 - Lösung: Vollständiges statisches Kanban-Board zusammenführen

## Aufgabe 1: Zusätzliche Tickets per Emmet

Emmet-Eingabe je Spalte, z. B. für "In Progress": `div.card.mb-2>div.card-body{Ticket C}`

```html
<div class="card mb-2">
  <div class="card-body">Ticket C</div>
</div>
```

## Aufgabe 2: Breitentest

| Breite | Sichtbare Spalten nebeneinander |
| ------ | ------------------------------- |
| 375px  | 1 (untereinander)               |
| 800px  | 3                               |
| 1200px | 3                               |

## Aufgabe 3: Build aktualisieren

```bash
npx gulp build
```

## Aufgabe 4: Referenz für Modul 18

Bei 800-1200px zeigt das Board drei farbig umrandete Spalten mit abgerundeten Ticket-Karten und Hover-Schatten - dieses Erscheinungsbild dient als visuelle Zielvorgabe für die React-Komponenten in Modul 18.

## Aufgabe 5: Commit

```bash
git add -A
git commit -m "feat: finalize static Kanban board layout"
```

## Grenzen

Das Board zeigt weiterhin nur statisch eingetragene Beispiel-Tickets - echte Daten aus der API kommen erst mit der React-Anbindung in Modul 19.
