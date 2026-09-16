# Transfer-Übung Modul 3 - Lösung: Zweite vollständige PR-Iteration

## Aufgabe 1-2: Branch und Commit

```bash
git checkout -b feature/board-styling-notes
# Kommentar in index.html ergänzen: <!-- TODO: styling in Modul 17 -->
git add index.html
git commit -m "docs: note future styling work"
```

## Aufgabe 3: Push und PR

```bash
git push -u origin feature/board-styling-notes
```

Beispiel-PR-Beschreibung:

> **Was:** ergänzt einen Platzhalter-Kommentar für zukünftiges Styling.
> **Warum:** dokumentiert sichtbar, dass Styling erst in Modul 17 folgt.
> **Wie testen:** `index.html` öffnen, Kommentar oberhalb der Board-Spalten im Quelltext prüfen.

## Aufgabe 4-5: Review, Merge, Aufräumen

Auf GitHub: reviewen, "Squash and Merge", "Delete branch" klicken.

```bash
git checkout main
git pull origin main
git branch -d feature/board-styling-notes
```

## Grenzen

Bei nur zwei Kursteilnehmenden übernimmt der Trainer bei Bedarf die zweite Reviewer-Rolle.
