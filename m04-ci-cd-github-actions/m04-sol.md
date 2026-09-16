# Transfer-Übung Modul 4 - Lösung: CI-Pipeline unter Realbedingungen testen

## Aufgabe 1-3: Fehlerfall provozieren und beheben

```bash
git checkout -b feature/ci-badge
# package.json: "lint": "exit 1" setzen
git add package.json
git commit -m "test: temporarily break lint script"
git push -u origin feature/ci-badge
# PR öffnen, roten Check beobachten

# package.json: "lint": "echo \"lint ok\"" zurücksetzen
git add package.json
git commit -m "fix: restore lint script"
git push
# grünen Check beobachten
```

## Aufgabe 4: Badge ergänzen

```md
## CI Status

![CI](https://github.com/<user>/teamboard/actions/workflows/ci.yml/badge.svg)
```

## Aufgabe 5: Merge

```bash
git add README.md
git commit -m "docs: add CI status badge"
git push
```

Auf GitHub: PR mergen ("Squash and Merge").

## Grenzen

Der Fehlerfall wird hier bewusst provoziert - in echten Projekten sollte `"lint": "exit 1"` nie absichtlich auf `main` gepusht werden.
