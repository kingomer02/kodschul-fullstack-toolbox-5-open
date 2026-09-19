# Transfer-Übung Modul 3 - Übung: Zweite vollständige PR-Iteration

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - zweiter kompletter Push-Branch-PR-Merge-Zyklus auf GitHub.

## Ziel

Den kompletten Remote-Workflow aus den drei GitHub-Labs (Push, Branching, Pull Requests) an einer zweiten, eigenständigen Änderung wiederholen, damit er zur Routine wird statt Einzelübung zu bleiben.

## Ausgangslage

- `main` auf GitHub enthält den gemergten Stand aus Lab 3.3 (`README.md`, dazu das HTML-Grundgerüst mit den Spaltenüberschriften aus Modul 2).

## Aufgaben

1. Erstelle einen neuen Branch `feature/board-styling-notes` ausgehend vom aktuellen `main`.
2. Ergänze in `index.html` einen HTML-Kommentar `<!-- TODO: styling in Modul 17 -->` oberhalb von `<div id="board">` und committe die Änderung.
3. Push den Branch, öffne einen PR mit Beschreibung nach dem Format aus Lab 3.3 (Was/Warum/Wie testen).
4. Führe ein Review durch (eigener Kommentar oder Partner-Review), merge per "Squash and Merge", lösche den Branch remote und lokal.
5. Aktualisiere lokal `main` (`git pull`).

## Checkpoint

- GitHub zeigt zwei erfolgreich gemergte Pull Requests in der Historie.
- Lokaler und remoter `main`-Branch sind identisch (`git status` zeigt "up to date").

## Abschlusskriterien

- `main` ist bereit für die CI-Pipeline aus Modul 4 - der Workflow Branch → PR → Review → Merge sitzt ohne Nachfragen.

## Fallback

Falls der PR-Check (falls schon vorhanden) rot ist: Ursache im PR-Log lesen, lokal korrigieren, erneut pushen - das ist bereits das Muster für Modul 4.
