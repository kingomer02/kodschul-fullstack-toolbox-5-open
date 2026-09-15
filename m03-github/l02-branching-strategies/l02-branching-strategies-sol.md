# Lab 3.2 - Lösung: Branching-Strategien im Team

## Aufgabe 1-2: Branch erstellen und ändern

```bash
git checkout -b feature/setup
# Kommentar in README.md ändern
git add README.md
git commit -m "docs: update project note on feature branch"
```

## Aufgabe 3: Konkurrierende Änderung auf `main`

```bash
git checkout main
# dieselbe Zeile anders ändern
git add README.md
git commit -m "docs: update project note on main"
```

## Aufgabe 4: Merge und Konfliktauflösung

```bash
git merge feature/setup
```

Git markiert die Konfliktstelle:

```text
<<<<<<< HEAD
Text-Version von main
=======
Text-Version von feature/setup
>>>>>>> feature/setup
```

Die Markierungen entfernen, die gewünschte Version behalten oder kombinieren, dann:

```bash
git add README.md
git commit
```

## Grenzen

Dieser Konflikt wurde absichtlich provoziert - reale Konflikte entstehen meist durch parallele Arbeit mehrerer Personen, nicht durch bewusst gegensätzliche Änderungen.
