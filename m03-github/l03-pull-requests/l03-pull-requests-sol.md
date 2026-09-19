# Lab 3.3 - Lösung: Pull Requests erstellen, reviewen und mergen

## Aufgabe 0-2: main pushen, Branch anlegen, PR erstellen

```bash
git push origin main

git checkout -b feature/readme
# README.md im Editor anlegen
git add README.md
git commit -m "docs: README für das Projekt angelegt"
git push -u origin feature/readme
```

Beispiel-PR-Beschreibung:

> **Was:** legt ein `README.md` für TeamBoard an.
> **Warum:** bisher gibt es nur `README-draft.md`, den Konzeptentwurf aus Modul 1. Wer das Repo öffnet, soll in zwei Sätzen wissen, worum es geht und was schon läuft.
> **Wie testen:** `README.md` auf GitHub öffnen - Projektbeschreibung, Statuswerte und der Abschnitt „Stand“ sind lesbar.

## Aufgabe 3: Review

Ein sinnvoller Reviewkommentar bezieht sich auf eine konkrete Zeile, z. B. „Der Abschnitt *Stand* sollte auch sagen, wie man sich das Ergebnis ansieht - also dass `index.html` im Browser geöffnet wird.“

## Aufgabe 4: Merge und Branch löschen

Auf GitHub: "Squash and Merge" wählen, Commit-Nachricht bestätigen, danach "Delete branch" klicken.

```bash
git checkout main
git pull origin main
git branch -d feature/readme
# meldet Git "not fully merged", ist -D richtig:
# der Squash-Merge ist ein neuer Commit mit anderem Hash
```

## Grenzen

Bei nur zwei Kursteilnehmenden ersetzt der Trainer bei Bedarf die zweite Reviewer-Rolle - der Ablauf bleibt identisch zu größeren Teams.
