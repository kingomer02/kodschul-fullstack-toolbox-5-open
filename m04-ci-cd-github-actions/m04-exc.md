# Transfer-Übung Modul 4 - Übung: CI-Pipeline unter Realbedingungen testen

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - schließt den Tag-1-Meilenstein (HTML-Grundgerüst + funktionierende CI) ab.

## Ziel

Die CI-Pipeline aus Lab 4.1/4.2 nicht nur einmal grün sehen, sondern bewusst durch einen Fehlerfall führen und wieder reparieren - das ist der Alltag, den die Pipeline abfangen soll.

## Ausgangslage

- `.github/workflows/ci.yml` mit `lint`- und `build`-Schritt aus Lab 4.2 liegt auf `main`.

## Aufgaben

1. Erstelle einen neuen Branch `feature/ci-badge`.
2. Ändere versehentlich (absichtlich) `"lint": "exit 1"` in `package.json`, committe und pushe. Öffne einen PR und beobachte den roten Check.
3. Setze das Lint-Skript im selben Branch wieder auf einen erfolgreichen Zustand zurück (z. B. `"echo \"lint ok\""`), committe erneut, push - beobachte den grünen Check.
4. Ergänze im Root-`README.md` einen Abschnitt "CI Status" mit einer Badge-Zeile: `![CI](https://github.com/<user>/teamboard/actions/workflows/ci.yml/badge.svg)`.
5. Merge den PR.

## Checkpoint

- Der PR zeigt in seiner Historie sowohl einen roten als auch einen grünen Check.
- `main` enthält nach dem Merge die CI-Badge-Zeile im README.

## Abschlusskriterien

- Tag-1-Ergebnis ist vollständig: HTML-Grundgerüst, vollständiger GitHub-Workflow, funktionierende und nachweislich fehlerempfindliche CI-Pipeline.

## Fallback

Falls der Check dauerhaft rot bleibt: lokal `npm run lint` und `npm run build` ausführen, um den Fehler außerhalb von GitHub Actions zu reproduzieren, bevor erneut gepusht wird.
