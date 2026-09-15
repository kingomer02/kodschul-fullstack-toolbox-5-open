# Lab 4.1 - Übung: Aufbau einer Workflow-Datei

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - diese Übung nutzt ein generisches Übungsrepo; die TeamBoard-Pipeline folgt in Lab 4.2.

## Ausgangslage

Ein beliebiges GitHub-Repo (z. B. ein leeres Übungsrepo) mit Push-Zugriff.

## Aufgaben

1. Lege im Übungsrepo den Ordner `.github/workflows/` an.
2. Erstelle darin `ci.yml` mit Trigger `on: push`, einem Job `build` auf `ubuntu-latest` und zwei Steps: `actions/checkout@v4` und einem `run`-Step, der eine beliebige Nachricht ausgibt.
3. Pushe die Datei und prüfe im "Actions"-Tab, dass der Workflow gelaufen ist und grün (erfolgreich) markiert wurde.
4. Ändere den Trigger so, dass der Workflow zusätzlich bei `pull_request` ausgelöst wird, und teste das mit einem Test-PR.

## Checkpoint

- `.github/workflows/ci.yml` existiert und referenziert `actions/checkout@v4`.
- Der Actions-Tab zeigt mindestens einen erfolgreichen Lauf.

## Abschlusskriterien

- Workflow läuft ohne Fehler bei Push und bei Pull Request.

## Fallback

Ohne eigenes Übungsrepo: eine vom Trainer bereitgestellte Vorlage forken und dort die Workflow-Datei ergänzen.
