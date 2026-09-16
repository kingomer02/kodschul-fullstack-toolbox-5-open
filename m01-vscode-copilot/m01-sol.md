# Transfer-Übung Modul 1 - Lösung: TeamBoard-Projektstart mit VS Code & Copilot

## Aufgabe 1: Projektordner

```bash
mkdir teamboard
mv README-draft.md teamboard/
```

## Aufgabe 2: `CONTRIBUTING.md`

```md
# Contributing

- Branches: `feature/<kurzbeschreibung>`
- Commits: `type: kurze Beschreibung` (z. B. `feat:`, `fix:`, `chore:`)
```

## Aufgabe 3: Abgleich mit der Wachstumstabelle

`teamboard/README-draft.md` sollte danach mindestens enthalten:

```md
## Ticket

- title: string
- description: string
- assignee: string
- status: "To Do" | "In Progress" | "Done"

## Actions

- create a ticket
- assign a ticket to a person
- change a ticket's status (move it between columns)
```

## Aufgabe 4: Copilot-Workflow-Wahl

Beispielantwort: Copilot Chat eignet sich für Text/Konzepte (README, Commit-Konventionen), bei denen ein ganzer Absatz auf einmal entsteht; Inline-Vorschläge eignen sich für Code, bei dem man Zeile für Zeile im bestehenden Kontext weiterschreibt.

## Grenzen

`teamboard/` ist zu diesem Zeitpunkt noch kein Git-Repository - `git init` erfolgt erst in Modul 2.
