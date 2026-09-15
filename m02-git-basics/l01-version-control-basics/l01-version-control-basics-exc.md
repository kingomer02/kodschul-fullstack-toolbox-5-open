# Lab 2.1 - Übung: Warum Versionskontrolle? Grundbegriffe

**Dauer:** ca. 15 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - generische Begriffsübung.

## Aufgaben

1. Erstelle einen leeren Ordner `git-uebung/` und initialisiere ihn mit `git init`.
2. Lege eine Datei `notiz.txt` mit dem Inhalt `Version 1` an und committe sie mit einer aussagekräftigen Nachricht.
3. Ändere `notiz.txt` zu `Version 2` und sieh dir mit `git diff` an, was sich geändert hat, **bevor** du committest.
4. Committe die Änderung und sieh dir die Historie mit `git log --oneline` an.

## Checkpoint

- `git log --oneline` zeigt zwei Commits.
- Du kannst erklären, was `git diff` vor dem zweiten Commit angezeigt hat.

## Abschlusskriterien

- Zwei Commits mit unterschiedlichem Inhalt von `notiz.txt` existieren im lokalen Repo.

## Fallback

Falls `git` lokal nicht installiert ist: Installation gemäß Betriebssystem nachholen (siehe Lab 1.1 Versionsprüfung) und die Übung danach nachholen.
