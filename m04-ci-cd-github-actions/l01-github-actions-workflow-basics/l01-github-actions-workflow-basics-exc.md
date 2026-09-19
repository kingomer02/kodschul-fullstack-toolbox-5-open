# Lab 4.1 - Übung: Aufbau einer Workflow-Datei

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - das CI-Grundgerüst entsteht im TeamBoard auf einem Branch und wird in Lab 4.2 erweitert.

> **Korrektur (Durchlauf 09/2026, Ö. Akgeyik):** Im Original nutzt diese Übung ein „Übungsrepo“, das im gesamten Kurs nirgends angelegt wird - der Begriff kommt sonst nur als Notfallplan für Teilnehmende ohne GitHub-Konto vor. Dazu läuft GitHub Actions ausschließlich serverseitig, ein lokaler Übungsordner scheidet also aus. **Wir arbeiten im TeamBoard-Repo auf dem Branch `feature/ci-setup`** - sachlich richtiger, weil Lab 4.2 exakt dieselbe Datei `.github/workflows/ci.yml` erweitert.

## Ausgangslage

Das TeamBoard-Repo auf GitHub (Modul 3) mit Push-Zugriff.

## Aufgaben

1. Lege im TeamBoard-Repo einen Branch `feature/ci-setup` an und darin den Ordner `.github/workflows/`.

> **Korrektur (Durchlauf 09/2026, Ö. Akgeyik):** Beim ersten Push einer Datei unter `.github/workflows/` verlangt GitHub am Personal Access Token zusätzlich die Berechtigung **`workflow`** - `repo` allein genügt nicht, der Push wird sonst abgelehnt.

2. Erstelle darin `ci.yml` mit Trigger `on: push`, einem Job `build` auf `ubuntu-latest` und zwei Steps: `actions/checkout@v7` und einem `run`-Step, der eine beliebige Nachricht ausgibt.
3. Pushe die Datei und prüfe im "Actions"-Tab, dass der Workflow gelaufen ist und grün (erfolgreich) markiert wurde.
4. Ändere den Trigger so, dass der Workflow zusätzlich bei `pull_request` ausgelöst wird, und teste das mit einem Test-PR.

## Checkpoint

- `.github/workflows/ci.yml` existiert und referenziert `actions/checkout@v7`.
- Der Actions-Tab zeigt mindestens einen erfolgreichen Lauf.

## Abschlusskriterien

- Workflow läuft ohne Fehler bei Push und bei Pull Request.

## Fallback

Falls der Push wegen fehlender `workflow`-Berechtigung scheitert: neuen Token mit den Haken `repo` **und** `workflow` erzeugen, dann erneut pushen.
