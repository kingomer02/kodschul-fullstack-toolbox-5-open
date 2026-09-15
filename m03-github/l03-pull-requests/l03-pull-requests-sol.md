# Lab 3.3 - Lösung: Pull Requests erstellen, reviewen und mergen

## Aufgabe 1-2: Branch pushen und PR erstellen

```bash
git push -u origin feature/setup
```

Beispiel-PR-Beschreibung:

> **Was:** fügt das HTML-Grundgerüst für TeamBoard hinzu.
> **Warum:** legt die Basis für die spätere React-Migration (Modul 18-19).
> **Wie testen:** `index.html` im Browser öffnen, drei leere Spalten (To Do/In Progress/Done) sind sichtbar.

## Aufgabe 3: Review

Ein sinnvoller Reviewkommentar bezieht sich auf eine konkrete Zeile, z. B. "Spaltentitel sollten exakt `To Do`/`In Progress`/`Done` lauten, damit sie später zum Status-Enum passen (Modul 7)."

## Aufgabe 4: Merge und Branch löschen

Auf GitHub: "Squash and Merge" wählen, Commit-Nachricht bestätigen, danach "Delete branch" klicken.

```bash
git checkout main
git pull origin main
git branch -d feature/setup
```

## Grenzen

Bei nur zwei Kursteilnehmenden ersetzt der Trainer bei Bedarf die zweite Reviewer-Rolle - der Ablauf bleibt identisch zu größeren Teams.
