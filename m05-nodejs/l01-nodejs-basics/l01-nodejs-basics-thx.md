# Modul 5: Node.js-Grundlagen

## Lab 5.1 - Grundlagen und Installation

---

## Lab-Ziel

Du verstehst, welche Rolle Node.js in der Webentwicklung spielt, und hast ein erstes Node.js-Skript ausgeführt.

**Leitfragen:**

<details>
<summary>Was ist Node.js, und warum kann JavaScript damit außerhalb des Browsers laufen?</summary>

Node.js ist eine JavaScript-Laufzeitumgebung auf Basis der V8-Engine, die JavaScript-Code direkt auf dem Server/Rechner ausführt, ohne Browser.

</details>

<details>
<summary>Wofür wird Node.js in diesem Kurs konkret gebraucht?</summary>

Als Backend-Laufzeit für die TeamBoard-API (REST/GraphQL) sowie als Werkzeug für Build-Tools (TypeScript-Compiler, Gulp, spätere Frontend-Tools).

</details>

<details>
<summary>Was ist der Unterschied zwischen synchronem und asynchronem Code in Node.js - warum ist das wichtig?</summary>

Node.js ist single-threaded mit einer Event-Loop; blockierende (synchrone) Operationen wie Dateizugriffe würden die gesamte Laufzeit anhalten, deshalb arbeiten I/O-Operationen meist asynchron (Callbacks/Promises).

</details>

---

## Node.js einordnen

- **Browser-JavaScript**: läuft in der JS-Engine des Browsers, hat Zugriff auf DOM/Window.
- **Node.js**: dieselbe Sprache, andere Laufzeitumgebung - kein DOM, dafür Dateisystem-, Netzwerk- und Prozesszugriff.

**Für TeamBoard:** das Backend (REST/GraphQL-API, Modul 14-16) läuft auf Node.js; das Frontend (Modul 18-19) läuft im Browser.

---

## Installation prüfen

```bash
node --version
npm --version
```

**Grenze:** dieser Kurs setzt eine bereits installierte Node.js-LTS-Version voraus (siehe Vorbereitungshinweise) - dieses Lab prüft nur, dass sie korrekt vorhanden ist.

---

## Erstes Node-Skript

```js
// hello.js
console.log("Node.js läuft:", process.version);
```

```bash
node hello.js
```

---

## Checkpoint

`node --version` liefert eine LTS-Version, und ein eigenes Skript wurde erfolgreich mit `node` ausgeführt.

Weiter geht es mit Lab 5.2: NPM/Yarn-Paketmanagement.
