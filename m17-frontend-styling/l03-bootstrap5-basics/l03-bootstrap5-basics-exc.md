# Lab 17.3 - Übung: Bootstrap 5: Grundlagen für die TeamBoard-Oberfläche

**Dauer:** ca. 35 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - legt den `frontend/`-Ordner mit dem ersten HTML-Grundgerüst an.

## Ausgangslage

- Es existiert noch kein `frontend/`-Ordner im Projekt.

## Aufgaben

1. Erstelle `frontend/index.html` mit Bootstrap 5 per CDN im `<head>` eingebunden.
2. Baue ein `div.container-fluid > div.row` mit drei Spalten (`col-12 col-md-4`) für "To Do", "In Progress", "Done".
3. Ergänze in der "To Do"-Spalte zwei Bootstrap-`card`-Elemente als Beispiel-Tickets (`card` + `card-body`).
4. Öffne die Datei im Browser und beobachte im responsiven Modus den Umbruch zwischen schmaler und "medium"-Breite.
5. Committe den neuen `frontend/`-Ordner.

## Checkpoint

- Auf schmalen Bildschirmen stehen die drei Spalten untereinander; ab "medium"-Breite (≥768px) stehen sie nebeneinander.

## Abschlusskriterien

- Kein eigenes CSS wurde für das Grundlayout geschrieben - ausschließlich Bootstrap-Klassen.

## Fallback

Falls das CDN im Schulungsnetzwerk nicht erreichbar ist: Bootstrap-CSS-Datei lokal herunterladen und per relativem Pfad statt CDN-Link einbinden.
