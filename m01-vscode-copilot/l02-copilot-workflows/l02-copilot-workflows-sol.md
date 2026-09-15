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

## Aufgabe 5: Spec-first vs. Prompt ohne Spec

Beispiel-Spec (vor dem Prompt notiert):

- Felder: Titel, Beschreibung, Zuständiger, Status
- Status-Werte: To Do, In Progress, Done
- Aktionen: erstellen, zuweisen, Status ändern

Mit dieser Spec als Grundlage trifft der Prompt aus Aufgabe 1 die Felder und Status-Werte in der Regel beim ersten Versuch genau, ohne Nachbesserung.

- Ohne Spec: der Vorschlag braucht meist noch eine Korrekturrunde (siehe Aufgabe 2).
- Diese Aufgabe ist ein reiner Prompt-Workflow (eine Anfrage, eine Antwort) - ein agentischer Workflow läge vor, wenn die KI selbstständig mehrere Dateien anlegen und verknüpfen würde.

## Grenzen

Der KI-generierte Text ist ein Entwurf; die endgültige Datenstruktur wird erst in Modul 7 (TypeScript-Interfaces) verbindlich.
