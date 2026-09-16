# Lab 17.2 - Übung: Responsives Design mit Grid und Flexbox

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - eigenständiges Beispiellayout.

## Vorbereitung

- Ein leerer Ordner `sample-layout/` mit `index.html` und `styles.css` liegt bereit.

## Aufgaben

1. Baue in `index.html` drei `div.column`-Elemente innerhalb eines `div.board` (Überschriften "To Do", "In Progress", "Done", je 1-2 `div.ticket`-Beispielelementen - nutze gern Emmet aus Lab 17.1).
2. Style `.board` mit CSS Grid, sodass die drei Spalten nebeneinanderstehen (`grid-template-columns: repeat(3, 1fr)`).
3. Style `.column` mit Flexbox (`flex-direction: column`), sodass die Tickets innerhalb einer Spalte untereinanderstehen.
4. Ergänze eine `@media (max-width: 600px)`-Regel, die `.board` auf eine einzelne Spalte umstellt.
5. Öffne `index.html` im Browser, aktiviere den responsiven Modus in den Entwicklertools und beobachte den Umbruch bei 600px.

## Checkpoint

- Über 600px Breite stehen die Spalten nebeneinander; unter 600px stehen sie untereinander.

## Abschlusskriterien

- Du kannst erklären, warum in diesem Beispiel Grid für `.board` und Flexbox für `.column` gewählt wurde, statt beides mit demselben Verfahren zu lösen.

## Fallback

Falls kein direkter Browserzugriff möglich ist: die Breitenänderung stattdessen durch manuelles Ändern der Fenstergröße des Editors/Browsers simulieren.
