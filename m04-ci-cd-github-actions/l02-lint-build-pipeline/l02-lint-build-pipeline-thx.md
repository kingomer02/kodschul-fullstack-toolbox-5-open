# Modul 4: Continuous Integration mit GitHub Actions

## Lab 4.2 - Lint- und Build-Pipeline für TeamBoard

---

## Lab-Ziel

Du hast für TeamBoard eine Actions-Pipeline eingerichtet, die bei jedem Push Node.js installiert, Abhängigkeiten installiert und Linting/Build ausführt.

**Leitfragen:**

<details>
<summary>Warum Node.js in der Pipeline explizit über `actions/setup-node` festlegen?</summary>

Der Runner hat keine feste Node-Version garantiert; `setup-node` stellt sicher, dass Pipeline und lokale Entwicklungsumgebung dieselbe Version nutzen.

</details>

<details>
<summary>Was bedeutet ein rotes ("failing") Actions-Ergebnis konkret?</summary>

Mindestens ein Step im Job ist mit einem Fehlercode beendet worden - der Job bricht ab und markiert den Lauf als fehlgeschlagen.

</details>

<details>
<summary>Wie hängen Caching und Pipeline-Geschwindigkeit zusammen?</summary>

`actions/setup-node` mit `cache: npm` speichert bereits heruntergeladene Pakete zwischen Läufen zwischen, was wiederholte `npm install`-Läufe deutlich beschleunigt.

</details>

---

## Node.js-Umgebung in der Pipeline

```yaml
- uses: actions/setup-node@v7
  with:
    node-version: 24
    cache: npm
- run: npm ci
```

- `npm ci` installiert exakt die in `package-lock.json` festgehaltenen Versionen - reproduzierbarer als `npm install`.

---

## Lint- und Build-Steps

```yaml
- run: npm run lint
- run: npm run build
```

**Grenze:** ohne passende `lint`/`build`-Skripte in `package.json` schlägt der Step sofort fehl - diese Skripte sind hier bewusst nur Platzhalter (`echo ...`) und werden in Lab 6.2 durch einen echten `tsc`-Build ersetzt, sobald das TypeScript-Setup steht. Die Workflow-Datei selbst ändert sich dabei nicht - nur der Inhalt der `package.json`-Skripte.

---

## Vollständiges Beispiel

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

---

## Checkpoint

Ein Push auf `main` löst eine grüne Pipeline aus, die Node.js installiert, Abhängigkeiten installiert und Lint/Build erfolgreich ausführt.

Weiter geht es mit Modul 5: Node.js-Grundlagen und Paketmanagement.
