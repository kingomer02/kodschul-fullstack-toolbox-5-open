# Transfer-Übung Modul 2 - Übung: Sauberer lokaler Verlauf für TeamBoard

**Dauer:** ca. 15 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - ergänzt zwei weitere Commits auf Basis von Lab 2.1-2.3.

## Ziel

Die drei Git-Labs (Repo anlegen, erster Commit, Status/Historie) zu einem mehrstufigen, sauberen lokalen Verlauf verbinden, der direkt nach Modul 3 auf GitHub gepusht werden kann.

## Ausgangslage

- Lokales `teamboard/`-Repo mit zwei Commits aus Lab 2.2/2.3 (README/Konzept, `<div id="board">`-Platzhalter).

## Aufgaben

1. Ergänze `index.html` um die drei Spalten-Überschriften `To Do`, `In Progress`, `Done` innerhalb von `<div id="board">` und committe dies als dritten Commit.
2. Lege eine `.gitignore`-Datei an (z. B. mit `node_modules/`, `.DS_Store`) und committe sie separat als vierten Commit.
3. Sieh dir `git log --oneline --graph` an und vergleiche mit `git diff <erster-commit> <letzter-commit>`, um den Gesamtfortschritt zu erkennen.
4. Prüfe mit `git status`, dass der Arbeitsbereich vollständig sauber ist (keine offenen Änderungen).

## Checkpoint

- `git log --oneline` zeigt mindestens 4 Commits.
- `git status` meldet "nothing to commit, working tree clean".

## Abschlusskriterien

- Das lokale Repo ist bereit, in Modul 3 per `git remote add origin ...` mit GitHub verbunden zu werden.

## Fallback

Bei einem fehlerhaften Commit **vor** einem eventuellen Push mit `git commit --amend` oder `git reset --soft HEAD~1` korrigieren - niemals `--hard` verwenden, solange die Änderung noch gebraucht wird.
