# Lab 4.1 - Lösung: Aufbau einer Workflow-Datei

## Aufgabe 1-2: Branch und Workflow-Datei

```bash
git checkout -b feature/ci-setup
```

`.github/workflows/ci.yml`:

```yaml
name: CI
on:
  push:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v7
      - run: echo "Hello CI"
```

## Aufgabe 3: Lauf prüfen

Nach `git push` erscheint im "Actions"-Tab ein neuer Lauf mit grünem Haken, sobald `echo "Hello CI"` fehlerfrei durchläuft.

## Aufgabe 4: Trigger erweitern

```yaml
on:
  push:
  pull_request:
```

Ein Test-Pull-Request (z. B. von einem Übungsbranch) löst danach denselben Workflow zusätzlich aus - sichtbar sowohl im PR selbst (Checks) als auch im Actions-Tab.

## Grenzen

Dieser Workflow prüft nichts Inhaltliches - er zeigt nur, dass CI überhaupt ausgelöst wird. Echtes Lint/Build folgt in Lab 4.2.
