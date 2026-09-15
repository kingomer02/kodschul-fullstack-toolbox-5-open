# Lab 2.3 - Lösung: Erste Commits, Status und Historie einsehen

## Aufgabe 1: `index.html` erweitern

```html
<body>
  <h1>TeamBoard</h1>
  <p>Kanban-Ticket-System - wird im Kursverlauf aufgebaut.</p>
  <div id="board"></div>
</body>
```

## Aufgabe 2: Status vor dem Staging

```bash
git status
```

Erwartet: `index.html` erscheint unter "Changes not staged for commit" (Kategorie: Modified).

## Aufgabe 3: Status nach dem Staging

```bash
git add index.html
git status
```

Erwartet: `index.html` erscheint jetzt unter "Changes to be committed" (Kategorie: Staged). Der Dateiinhalt hat sich nicht geändert - nur die Git-interne Markierung.

## Aufgabe 4: Commit

```bash
git commit -m "Board-Platzhalter in index.html ergänzt"
```

## Aufgabe 5: Commit-Details ansehen

```bash
git log --oneline
git show <commit-hash>
```

Erwartete Ausgabe von `git show`: Autor, Datum, Commit-Nachricht und ein Diff, das nur die neue `<div id="board">`-Zeile als Addition zeigt.

## Grenzen

`git commit --amend` (Fallback) darf nur vor einem Push verwendet werden - danach verändert es bereits geteilte Historie, was in Modul 3 zu Konflikten führen kann.
