# Lab 2.3 - Übung: Erste Commits, Status und Historie einsehen

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - ergänzt einen zweiten Commit.

## Vorbereitung

- Das TeamBoard-Repo aus Lab 2.2 mit genau einem Commit liegt lokal vor.

## Aufgaben

1. Ergänze `index.html` um eine leere `<div id="board"></div>` als Platzhalter für das spätere Board.
2. Führe `git status` **vor** dem Staging aus und notiere, welche Kategorie die Änderung zeigt.
3. Stage die Änderung, führe `git status` erneut aus und vergleiche die Ausgabe.
4. Committe die Änderung mit einer aussagekräftigen Nachricht.
5. Zeige dir mit `git show <commit-hash>` die Details deines zweiten Commits an.

## Checkpoint

- `git log --oneline` zeigt zwei Commits.
- Du kannst den Unterschied zwischen den beiden `git status`-Ausgaben (Aufgabe 2 vs. 3) benennen.

## Abschlusskriterien

- Zweiter Commit existiert und enthält ausschließlich die `<div id="board">`-Änderung.

## Fallback

Falls versehentlich zu früh committet wurde: mit `git commit --amend` die letzte Commit-Nachricht oder den Inhalt korrigieren, solange noch nicht gepusht wurde.
