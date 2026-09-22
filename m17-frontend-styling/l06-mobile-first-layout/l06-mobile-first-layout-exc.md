# Lab 17.6 - Übung: Mobile first, Layout ohne Breakpoints, Container Queries

**Dauer:** ca. 40 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - Weiterentwicklung des Beispiellayouts aus Lab 17.2 in `sample-layout/`.

## Ausgangslage

- `sample-layout/` aus Lab 17.2: drei Spalten mit Grid, eine Media Query bei 600px.

## Aufgaben

1. **Umbau auf mobile first.** Schreib `styles.css` so um, dass die Grundregeln für ein schmales Handy gelten. Wie viele Regeln brauchst du jetzt noch für breite Bildschirme?
2. **Weg mit der Media Query.** Ersetze das feste Spaltenlayout durch eine Grid-Definition, die selbst entscheidet, wie viele Spalten hineinpassen. Eine Spalte soll nie schmaler als etwa 16rem werden.
3. **Bessere Karten.** Gib jeder Ticketkarte Titel, Beschreibung, Zuständige und einen Button "Weiter →". In einer schmalen Spalte steht alles untereinander. In einer breiten Spalte stehen Titel und Beschreibung links, Zuständige und Button rechts. Entscheide nach der Breite der **Spalte**, nicht des Bildschirms.
4. Die Überschrift soll mit der Fensterbreite stufenlos wachsen, aber nie kleiner als 1.5rem und nie größer als 2.5rem werden.
5. Buttons brauchen auf Touch-Geräten eine Mindesthöhe von 44px.
6. **Prüfen** in den Entwicklertools bei 375px, 700px und 1200px: Wie viele Spalten? Wie sieht die Karte aus? Schau dir bei 1200px im Grid-Inspektor die Spuren an.
7. **Experiment:** Tausche `auto-fit` gegen `auto-fill` und vergleiche bei 1200px. Was passiert mit den Karten - und warum?

## Checkpoint

- 375px: eine Spalte · 700px: zwei Spalten, "Done" rutscht in die zweite Zeile · 1200px: drei Spalten.
- Die Karte ist nur bei 1200px zweispaltig.
- `styles.css` enthält keine `@media`-Regel für das Board.

## Abschlusskriterien

- Du kannst erklären, warum die Karte bei 700px einspaltig bleibt, obwohl der Bildschirm breiter ist als bei 375px.
- Du kannst den Unterschied zwischen `auto-fit` und `auto-fill` an deinem Experiment erklären.

## Fallback

Falls die Container Query nie greift: Hat das **Elternelement** der Karte `container-type: inline-size`? Die Karte selbst kann nicht ihr eigener Container sein.
