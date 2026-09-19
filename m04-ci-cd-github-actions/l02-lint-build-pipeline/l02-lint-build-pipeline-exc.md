# Lab 4.2 - Übung: Lint- und Build-Pipeline für TeamBoard

**Dauer:** ca. 40 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - TeamBoard erhält seine erste CI-Pipeline.

## Ausgangslage

Das TeamBoard-Repo auf GitHub (Modul 3) enthält bisher nur statisches HTML/CSS, noch kein Node.js-Projekt.

## Aufgaben

1. Lege im TeamBoard-Repo minimal ein `package.json` an (z. B. via `npm init -y`) mit den Skripten `lint` (z. B. `echo "lint ok"` als Platzhalter) und `build` (z. B. `echo "build ok"` als Platzhalter). Erzeuge anschließend die Lock-Datei mit `npm install --package-lock-only`.

> **Warum der zweite Befehl nötig ist:** `npm init -y` erzeugt **keine** `package-lock.json`, und ohne installierte Abhängigkeit entsteht auch keine. `npm ci` in Aufgabe 2 bricht dann ab mit `npm error The \`npm ci\` command can only install with an existing package-lock.json`. `npm install --package-lock-only` erzeugt die Datei, ohne Pakete zu installieren. Genau dieser Fehler begegnet euch später im eigenen Projekt wieder - es lohnt sich, die Meldung einmal gesehen zu haben.
2. Erweitere die in Lab 4.1 angelegte `.github/workflows/ci.yml` zur echten Pipeline - Trigger `push`/`pull_request`, Checkout, `actions/setup-node@v7` (Node 24, `cache: npm`), `npm ci`, `npm run lint`, `npm run build`.
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
