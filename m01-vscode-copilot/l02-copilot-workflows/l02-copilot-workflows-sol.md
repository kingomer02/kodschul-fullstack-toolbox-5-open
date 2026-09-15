# Lab 1.2 - Lösung: KI-gestützte Entwicklung mit Copilots

## Aufgabe 1-2: Prompt und Korrektur

Beispielprompt:

> Erstelle ein Markdown-Konzept für ein minimales Kanban-Ticket-System namens TeamBoard. Ein Ticket hat Titel, Beschreibung, Zuständigen und Status. Status-Werte: To Do, In Progress, Done. Aktionen: Ticket erstellen, zuweisen, Status ändern. Nur Konzept, kein Code.

Typische Korrektur: Ein erster KI-Vorschlag listet Status oft als freien Text statt als feste Werte-Menge auf - das muss auf genau die drei Werte `To Do`, `In Progress`, `Done` präzisiert werden, da spätere Module (z. B. Modul 7) diese als Union-Type modellieren.

## Aufgabe 3: `README-draft.md`

```md
# TeamBoard (starter)

TeamBoard is a minimal Kanban ticket system built across this course.

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

Diese Struktur entspricht `output/project/starter/README-draft.md` und `output/project/contracts/ticket-contract.md`.

## Aufgabe 4: gezielterer Prompt

> Liste nur die drei Status-Werte für ein Kanban-Ticket als YAML-Liste.

Ein enger gefasster Prompt liefert typischerweise eine kürzere, direkter verwertbare Antwort - Beleg dafür, dass Prompt-Präzision die Nacharbeit reduziert.

## Grenzen

Der KI-generierte Text ist ein Entwurf; die endgültige Datenstruktur wird erst in Modul 7 (TypeScript-Interfaces) verbindlich.
