# Lab 17.4 - Übung: Sass-Grundlagen für eigene Farben und Abstände

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - ergänzt eine erste `.scss`-Datei im `frontend/`-Ordner.

## Ausgangslage

- `frontend/index.html` mit Bootstrap-Grundgerüst (Lab 17.3) liegt vor.

## Aufgaben

1. Erstelle `frontend/styles/main.scss` mit drei Farbvariablen (`$todo-color`, `$in-progress-color`, `$done-color`) und einer Variable `$ticket-radius`.
2. Ergänze eine `.column`-Regel mit verschachtelten `&.todo`, `&.in-progress`, `&.done`-Selektoren, die jeweils einen farbigen oberen Rahmen setzen.
3. Ergänze eine `.ticket`-Regel mit `border-radius: $ticket-radius` und einem verschachtelten `&:hover` für einen leichten Schatten.
4. Ergänze in `index.html` die passenden Klassen (`column todo`, `column in-progress`, `column done`) an den drei Spalten-Divs aus Lab 17.3.
5. Notiere (ohne sie auszuführen), welchen Befehl du in Lab 17.5 brauchen wirst, um diese `.scss`-Datei in echtes CSS umzuwandeln.

## Checkpoint

- `main.scss` enthält mindestens drei Variablen und mindestens zwei verschachtelte `&`-Selektoren.

## Abschlusskriterien

- `index.html` referenziert die drei Spalten bereits mit den neuen Klassennamen, auch wenn das CSS noch nicht kompiliert ist.

## Fallback

Falls unklar ist, welche Bootstrap-Klassen mit den neuen Klassen kombiniert werden sollen: neue Klassen einfach zusätzlich zu den bestehenden `col-12 col-md-4`-Klassen im `class`-Attribut ergänzen.
