# Lab 4.2 - Lösung: Lint- und Build-Pipeline für TeamBoard

## Aufgabe 1: `package.json`

```bash
npm init -y
```

```json
{
  "scripts": {
    "lint": "echo \"lint ok\"",
    "build": "echo \"build ok\""
  }
}
```

## Aufgabe 2: Workflow-Datei

`.github/workflows/ci.yml`:

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
      - uses: actions/checkout@v7
      - uses: actions/setup-node@v7
        with:
          node-version: 24
          cache: npm
      - run: npm ci
      - run: npm run lint
      - run: npm run build
```

## Aufgabe 3-4: PR und Merge

```bash
git checkout -b feature/ci-pipeline
git add package.json package-lock.json .github/workflows/ci.yml
git commit -m "ci: add lint/build pipeline"
git push -u origin feature/ci-pipeline
```

Auf GitHub: PR öffnen, warten bis der Check grün ist, dann mergen (Squash and Merge, wie in Lab 3.3 geübt).

## Gegentest (optional)

`"lint": "exit 1"` probeweise setzen, pushen, beobachten, dass die Pipeline rot wird - danach wieder auf ein erfolgreiches Skript zurücksetzen.

## Grenzen

Die Lint/Build-Skripte sind hier noch Platzhalter; ab Modul 6 (TypeScript-Setup) ersetzt `tsc`/ein echter Linter diese Platzhalter ohne Änderung an der Workflow-Datei selbst.
