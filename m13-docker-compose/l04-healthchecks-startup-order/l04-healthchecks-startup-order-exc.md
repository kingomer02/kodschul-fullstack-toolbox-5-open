# Lab 13.4 - Übung: Healthchecks und Startreihenfolge

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - `docker-compose.yml` bekommt einen Healthcheck für `mongo`.

## Ausgangslage

- Lab 14.3 ist abgeschlossen: Das Backend läuft als Express-Server im Container, `docker-compose.yml` hat `ports` und `depends_on` in der kurzen Listenform.

> **Warum erst nach Lab 14.3:** Vorher ist das Backend ein Skript, das sofort wieder endet. Die Startreihenfolge sieht man erst, wenn es dauerhaft läuft.

## Aufgaben

1. Ergänze beim Service `mongo` einen `healthcheck`. Der Test soll MongoDB fragen, ob sie antwortet. Welchen Befehl du dafür im Container ausführst, findest du selbst heraus (Hinweis im Theorieteil).
2. Stelle `depends_on` beim `backend` so um, dass es auf einen **gesunden** `mongo` wartet.
3. Starte neu mit `docker compose down` und `docker compose up -d` und lies die Ausgabe Zeile für Zeile: In welcher Reihenfolge passiert was?
4. Mach den Healthcheck absichtlich kaputt (ein Test, der immer fehlschlägt) und beobachte, was `docker compose up -d` jetzt meldet. Danach wieder reparieren.
5. Committe die Änderung.

## Checkpoint

- Die Startausgabe zeigt `Waiting` und `Healthy` für `mongo`, bevor `backend` startet.
- `docker compose ps` zeigt `mongo` als `(healthy)`.

## Abschlusskriterien

- Du kannst erklären, was der Unterschied zwischen `condition: service_started` (Standard) und `condition: service_healthy` ist.
- Du kannst sagen, was mit `backend` passiert, wenn `mongo` nie gesund wird.

## Fallback

Falls der Test nie gesund wird: den Befehl erst von Hand ausprobieren - `docker compose exec mongo <dein-befehl>` - und den Exit-Code mit `echo $?` prüfen.
