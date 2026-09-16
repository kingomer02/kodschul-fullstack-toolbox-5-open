# Lab 13.3 - Lösung: Ausblick Container in der CI-Pipeline

## Aufgabe 1: Workflow ergänzen

```yaml
# .github/workflows/ci.yml (Ausschnitt)
- run: npm ci
- run: npm run lint
- run: npm run build
- run: docker compose config
```

## Aufgabe 2-4: Branch, PR, Merge

```bash
git checkout -b ci/validate-compose
git add .github/workflows/ci.yml
git commit -m "ci: validate docker-compose.yml on every push"
git push -u origin ci/validate-compose
```

Auf GitHub: PR öffnen, grünen Check abwarten, "Squash and Merge".

## Grenzen

Ein absichtlicher Syntaxfehler in `docker-compose.yml` (z. B. falsche Einrückung) lässt diesen Schritt rot werden, während `lint`/`build` weiterhin grün bleiben - ein Beleg dafür, dass der neue Schritt tatsächlich etwas Eigenständiges prüft.
