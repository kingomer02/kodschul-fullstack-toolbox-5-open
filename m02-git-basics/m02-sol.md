# Transfer-Übung Modul 2 - Lösung: Sauberer lokaler Verlauf für TeamBoard

## Aufgabe 1: Spaltenüberschriften committen

```bash
git add index.html
git commit -m "feat: add board column headers"
```

## Aufgabe 2: `.gitignore` committen

```bash
git add .gitignore
git commit -m "chore: add .gitignore"
```

## Aufgabe 3: Historie und Diff ansehen

```bash
git log --oneline --graph
git diff <erster-commit> <letzter-commit>
```

## Aufgabe 4: Sauberkeit prüfen

```bash
git status
# nothing to commit, working tree clean
```

## Grenzen

`git commit --amend`/`git reset --soft` sind nur vor einem Push sicher - danach verändern sie bereits geteilte Historie (relevant ab Modul 3).
