# GitHub-Actions-Cheatsheet

Schnellreferenz für die in Modul 4 (Workflow-Grundlagen, Lint/Build-Pipeline) verwendeten Bausteine.

## Dateiort und Grundstruktur

- Workflow-Dateien liegen unter `.github/workflows/*.yml` - jede `.yml`-Datei dort ist ein eigenständiger Workflow.

```yaml
name: CI
on:
  push:
    branches: [main]
  pull_request:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo "Hello CI"
```

## Trigger (`on`)

| Trigger             | Auslöser                                     |
| ------------------- | -------------------------------------------- |
| `push`              | Commit wird auf einen Branch gepusht         |
| `pull_request`      | Pull Request wird erstellt oder aktualisiert |
| `workflow_dispatch` | manueller Start über die GitHub-Oberfläche   |

## Häufig genutzte Actions

| Action                  | Zweck                                                                   |
| ----------------------- | ----------------------------------------------------------------------- |
| `actions/checkout@v4`   | Repo-Inhalt in den Runner auschecken                                    |
| `actions/setup-node@v4` | Node.js-Version installieren (Option `cache: npm` für schnellere Läufe) |

## Node/NPM-Pipeline-Bausteine

```yaml
- uses: actions/setup-node@v4
  with:
    node-version: 20
    cache: npm
- run: npm ci
- run: npm run lint
- run: npm run build
```

| Befehl          | Zweck                                                        |
| --------------- | ------------------------------------------------------------ |
| `npm ci`        | reproduzierbare Installation exakt gemäß `package-lock.json` |
| `npm run lint`  | konfiguriertes Lint-Skript ausführen                         |
| `npm run build` | konfiguriertes Build-Skript ausführen                        |

## Ergebnisse prüfen

| Wo                    | Was                                               |
| --------------------- | ------------------------------------------------- |
| Tab "Actions" im Repo | alle Läufe, Status (grün/rot), Logs je Step       |
| Pull-Request-Seite    | Checks-Bereich zeigt denselben Lauf im PR-Kontext |

## Faustregeln

- Ein fehlgeschlagener Step bricht den Job ab - Logs im jeweiligen Step zeigen die Fehlerursache.
- `npm ci` statt `npm install` in CI verwenden, sobald eine `package-lock.json` existiert.
- Denselben Workflow für `push` und `pull_request` triggern, damit auch offene PRs geprüft werden.
