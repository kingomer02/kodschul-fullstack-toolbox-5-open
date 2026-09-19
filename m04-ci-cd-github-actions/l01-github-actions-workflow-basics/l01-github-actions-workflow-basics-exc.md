# Lab 4.1 - Übung: Aufbau einer Workflow-Datei

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - das CI-Grundgerüst entsteht im TeamBoard auf einem Branch und wird in Lab 4.2 erweitert.

> **Hinweis:** GitHub Actions läuft ausschließlich auf GitHub, nicht lokal - die Workflow-Datei muss also in einem Repo mit Remote liegen. Wir arbeiten im TeamBoard auf dem Branch `feature/ci-setup`: Lab 4.2 erweitert genau dieselbe Datei `.github/workflows/ci.yml` zur echten Pipeline.

## Ausgangslage

Das TeamBoard-Repo auf GitHub (Modul 3) mit Push-Zugriff.

## Aufgaben

1. Lege im TeamBoard-Repo einen Branch `feature/ci-setup` an und darin den Ordner `.github/workflows/`.
2. Erstelle darin `ci.yml` mit Trigger `on: push`, einem Job `build` auf `ubuntu-latest` und zwei Steps: `actions/checkout@v7` und einem `run`-Step, der eine beliebige Nachricht ausgibt.
3. Pushe die Datei und prüfe im "Actions"-Tab, dass der Workflow gelaufen ist und grün (erfolgreich) markiert wurde.
4. Ändere den Trigger so, dass der Workflow zusätzlich bei `pull_request` ausgelöst wird, und teste das mit einem Test-PR.

> **Achtung beim ersten Push:** Sobald eine Datei unter `.github/workflows/` liegt, verlangt GitHub am Personal Access Token zusätzlich die Berechtigung **`workflow`**. `repo` allein genügt nicht - der Push wird sonst abgelehnt.

## Checkpoint

- `.github/workflows/ci.yml` existiert und referenziert `actions/checkout@v7`.
- Der Actions-Tab zeigt mindestens einen erfolgreichen Lauf.

## Abschlusskriterien

- Workflow läuft ohne Fehler bei Push und bei Pull Request.

## Fallback

Falls der Push wegen fehlender `workflow`-Berechtigung scheitert: neuen Token mit den Haken `repo` **und** `workflow` erzeugen, dann erneut pushen.
