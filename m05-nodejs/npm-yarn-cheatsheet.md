# NPM/Yarn-Cheatsheet

Schnellreferenz für die in Modul 5 (Paketmanagement) verwendeten Befehle.

## Projekt initialisieren

| NPM           | Yarn           | Wirkung                                        |
| ------------- | -------------- | ---------------------------------------------- |
| `npm init -y` | `yarn init -y` | neue `package.json` mit Standardwerten anlegen |

## Pakete installieren

| NPM                            | Yarn                             | Wirkung                                                    |
| ------------------------------ | -------------------------------- | ---------------------------------------------------------- |
| `npm install <pkg>`            | `yarn add <pkg>`                 | Paket als `dependency` installieren                        |
| `npm install --save-dev <pkg>` | `yarn add --dev <pkg>`           | Paket als `devDependency` installieren                     |
| `npm install`                  | `yarn install`                   | alle Abhängigkeiten gemäß `package.json` installieren      |
| `npm ci`                       | `yarn install --frozen-lockfile` | reproduzierbare Installation exakt gemäß Lockfile (für CI) |

## Pakete entfernen und aktualisieren

| NPM                   | Yarn                | Wirkung                                            |
| --------------------- | ------------------- | -------------------------------------------------- |
| `npm uninstall <pkg>` | `yarn remove <pkg>` | Paket entfernen                                    |
| `npm outdated`        | `yarn outdated`     | veraltete Abhängigkeiten anzeigen                  |
| `npm update`          | `yarn upgrade`      | Abhängigkeiten gemäß Versionsbereich aktualisieren |

## Skripte

| Befehl             | Wirkung                                               |
| ------------------ | ----------------------------------------------------- |
| `npm run <script>` | in `package.json` definiertes Skript ausführen        |
| `yarn <script>`    | dasselbe Skript mit Yarn ausführen (kein `run` nötig) |

## Lockfiles

| Datei               | Werkzeug | Zweck                                    |
| ------------------- | -------- | ---------------------------------------- |
| `package-lock.json` | NPM      | exakte installierte Versionen festhalten |
| `yarn.lock`         | Yarn     | dasselbe Prinzip für Yarn                |

**Grenze:** NPM und Yarn nicht gemischt im selben Projekt verwenden - immer nur ein Lockfile-Format pro Repo pflegen.

## `dependencies` vs. `devDependencies`

| Kategorie         | Beispiel                        | Wird gebraucht                         |
| ----------------- | ------------------------------- | -------------------------------------- |
| `dependencies`    | `express`                       | zur Laufzeit der Anwendung             |
| `devDependencies` | `typescript`, Linter, Testtools | nur während der Entwicklung/des Builds |

## Faustregeln

- `node_modules/` gehört nie ins Git-Repo (`.gitignore`).
- In CI immer `npm ci`/`yarn install --frozen-lockfile` statt `npm install` verwenden.
