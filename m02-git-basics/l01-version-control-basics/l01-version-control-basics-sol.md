# Lab 2.1 - Lösung: Warum Versionskontrolle? Grundbegriffe

## Aufgabe 1: Repo initialisieren

```bash
mkdir git-uebung && cd git-uebung
git init
```

Erwartete Ausgabe: `Initialized empty Git repository in .../git-uebung/.git/`

## Aufgabe 2: Erster Commit

```bash
echo "Version 1" > notiz.txt
git add notiz.txt
git commit -m "Erste Version der Notiz"
```

## Aufgabe 3: Diff vor dem Commit

```bash
echo "Version 2" > notiz.txt
git diff
```

Erwartete Ausgabe (vereinfacht):

```diff
- Version 1
+ Version 2
```

Das Minus zeigt die entfernte, das Plus die neue Zeile - genau das, was `git diff` als "Änderung gegenüber dem letzten Commit" versteht.

## Aufgabe 4: Zweiter Commit und Historie

```bash
git add notiz.txt
git commit -m "Notiz auf Version 2 aktualisiert"
git log --oneline
```

Erwartete Ausgabe: zwei Zeilen, je eine pro Commit, mit Kurz-Hash und Commit-Nachricht.

## Grenzen

Diese Übung zeigt lokale Historie. Das Teilen dieser Historie mit anderen (Push/Pull) ist Thema von Modul 3.
