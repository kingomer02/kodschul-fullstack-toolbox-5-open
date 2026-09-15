# Modul 4: Continuous Integration mit GitHub Actions

## Lab 4.1 - Aufbau einer Workflow-Datei

---

## Lab-Ziel

Du kannst eine GitHub-Actions-Workflow-Datei lesen und eine eigene, einfache Workflow-Datei schreiben.

**Leitfragen:**

<details>
<summary>Was ist Continuous Integration (CI), und welches Problem löst es?</summary>

CI führt bei jeder Änderung automatisch Prüfungen (z. B. Build, Lint, Tests) aus, statt Fehler erst spät oder manuell zu entdecken.

</details>

<details>
<summary>Aus welchen drei Bausteinen besteht eine GitHub-Actions-Workflow-Datei?</summary>

Trigger (`on`), Jobs und darin Steps - der Trigger bestimmt wann, Jobs/Steps bestimmen was ausgeführt wird.

</details>

<details>
<summary>Wo liegt eine Workflow-Datei im Repo, und woran erkennt GitHub sie?</summary>

Unter `.github/workflows/*.yml` - GitHub erkennt jede YAML-Datei in diesem Ordner automatisch als Workflow.

</details>

---

## CI-Grundidee

- Ohne CI: Fehler werden oft erst bemerkt, wenn jemand anderes den Code auscheckt oder ihn in Produktion nutzt.
- Mit CI: jeder Push löst automatisch Build/Lint/Tests aus, Ergebnis ist sofort auf GitHub sichtbar.

---

## Aufbau einer Workflow-Datei

```yaml
name: CI
on:
  push:
    branches: [main]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo "Hello CI"
```

| Baustein | Bedeutung                                                                     |
| -------- | ----------------------------------------------------------------------------- |
| `on`     | Trigger-Ereignis (z. B. `push`, `pull_request`)                               |
| `jobs`   | eine oder mehrere parallel/abhängig laufende Aufgaben                         |
| `steps`  | einzelne Befehle oder wiederverwendbare Actions (`uses`) innerhalb eines Jobs |

---

## Checkpoint

Eine Workflow-Datei mit Trigger, einem Job und mindestens zwei Steps wurde geschrieben und läuft nach einem Push sichtbar unter dem "Actions"-Tab.

Weiter geht es mit Lab 4.2: eine Lint/Build-Pipeline einrichten.
