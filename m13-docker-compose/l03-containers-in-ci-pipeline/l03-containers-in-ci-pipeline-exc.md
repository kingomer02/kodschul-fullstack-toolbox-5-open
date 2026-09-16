# Lab 13.3 - Übung: Ausblick Container in der CI-Pipeline

**Dauer:** ca. 15 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - ergänzt einen Validierungsschritt in der bestehenden CI-Pipeline.

## Ausgangslage

- `.github/workflows/ci.yml` aus Modul 4 mit `lint`- und `build`-Schritt; `docker-compose.yml` aus Lab 13.2 liegt im Projekt-Root.

## Aufgaben

1. Ergänze in `.github/workflows/ci.yml` nach dem bestehenden `build`-Schritt einen neuen Schritt: `run: docker compose config`.
2. Erstelle einen Branch, committe die Änderung, push und öffne einen PR.
3. Beobachte im PR-Check, dass der neue Schritt erfolgreich durchläuft.
4. Merge den PR nach erfolgreichem Check.

## Checkpoint

- Der GitHub-Actions-Lauf zeigt einen zusätzlichen grünen Schritt für `docker compose config`.

## Abschlusskriterien

- `main` enthält die aktualisierte `ci.yml`; ein absichtlich kaputter YAML-Syntaxfehler in `docker-compose.yml` würde diesen Schritt zuverlässig rot werden lassen (optional zum Testen).

## Fallback

Falls der GitHub-Actions-Runner kein Docker mit Compose-Plugin bereitstellt: `docker-compose config` (mit Bindestrich, Standalone-Variante) als Alternative im Workflow verwenden.
