# Lab 4.2 - Übung: Lint- und Build-Pipeline für TeamBoard

**Dauer:** ca. 40 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - TeamBoard erhält seine erste CI-Pipeline.

## Ausgangslage

Das TeamBoard-Repo auf GitHub (Modul 3) enthält bisher nur statisches HTML/CSS, noch kein Node.js-Projekt.

## Aufgaben

1. Lege im TeamBoard-Repo minimal ein `package.json` an (z. B. via `npm init -y`) mit den Skripten `lint` (z. B. `echo "lint ok"` als Platzhalter) und `build` (z. B. `echo "build ok"` als Platzhalter).
2. Erstelle `.github/workflows/ci.yml` mit Trigger `push`/`pull_request`, Checkout, `actions/setup-node@v4` (Node 20, `cache: npm`), `npm ci`, `npm run lint`, `npm run build`.
3. Committe und pushe auf einem Feature-Branch, eröffne einen Pull Request und prüfe, dass die Pipeline im PR als Check erscheint und grün wird.
4. Merge den PR über GitHub.

## Checkpoint

- Der Actions-Tab zeigt einen erfolgreichen Lauf für `lint` und `build`.
- Der PR-Check ist grün, bevor gemerged wird.

## Abschlusskriterien

- `npm ci` läuft ohne Fehler (gültige `package-lock.json` vorhanden).
- Pipeline schlägt sichtbar fehl, wenn absichtlich ein Platzhalter-Skript mit Exit-Code ≠ 0 getestet wird (kurzer Gegentest empfohlen).

## Fallback

Ohne lauffähiges echtes Lint-Tool: Platzhalter-Skripte (`echo ...`) genügen für dieses Lab - echtes Linting kommt mit dem TypeScript-Setup in Modul 6.
