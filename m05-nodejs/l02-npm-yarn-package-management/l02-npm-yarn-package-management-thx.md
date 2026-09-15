# Modul 5: Node.js-Grundlagen

## Lab 5.2 - NPM/Yarn-Paketmanagement

---

## Lab-Ziel

Du kannst ein Node.js-Projekt initialisieren, Pakete installieren und zwischen Produktions- und Entwicklungsabhängigkeiten unterscheiden.

**Leitfragen:**

<details>
<summary>Was steht in `package.json`, und wofür ist `package-lock.json`?</summary>

`package.json` beschreibt Projektmetadaten, Skripte und Abhängigkeiten mit Versionsbereichen; `package-lock.json` fixiert die exakten installierten Versionen für reproduzierbare Installationen.

</details>

<details>
<summary>Was ist der Unterschied zwischen `dependencies` und `devDependencies`?</summary>

`dependencies` werden zur Laufzeit gebraucht (z. B. Express); `devDependencies` nur während der Entwicklung (z. B. TypeScript, Linter, Testtools).

</details>

<details>
<summary>Warum landet `node_modules/` nicht im Git-Repo?</summary>

Der Ordner ist groß, plattformabhängig und vollständig aus `package.json`/`package-lock.json` reproduzierbar - er gehört in `.gitignore`.

</details>

---

## Projekt initialisieren

```bash
npm init -y
```

Erzeugt eine `package.json` mit Standardwerten, die anschließend angepasst werden kann.

---

## Pakete installieren

```bash
npm install express
npm install --save-dev typescript
```

| Befehl                         | Zielort in `package.json` |
| ------------------------------ | ------------------------- |
| `npm install <pkg>`            | `dependencies`            |
| `npm install --save-dev <pkg>` | `devDependencies`         |

**NPM vs. Yarn:** beide verwalten dieselben `package.json`-Abhängigkeiten; Yarn nutzt `yarn.lock` statt `package-lock.json` und teils andere Befehle (`yarn add` statt `npm install`).

---

## `.gitignore` für Node-Projekte

```text
node_modules/
dist/
.env
```

---

## Checkpoint

Ein `package.json` mit mindestens einer `dependency` und einer `devDependency` existiert; `node_modules/` ist über `.gitignore` vom Commit ausgeschlossen.

Weiter geht es mit Modul 6: Einführung in TypeScript.
