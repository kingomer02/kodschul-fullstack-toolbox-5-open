# Modul 6: Einführung in TypeScript

## Lab 6.1 - ECMAScript-Entwicklung und Vorteile von TypeScript

---

## Lab-Ziel

Du kennst die Motivation hinter TypeScript und hast ein kleines JavaScript-Skript nach TypeScript migriert.

**Leitfragen:**

<details>
<summary>Was ist TypeScript im Verhältnis zu JavaScript?</summary>

TypeScript ist eine Obermenge von JavaScript mit statischer Typprüfung; es wird zu reinem JavaScript kompiliert (transpiliert), bevor es ausgeführt wird.

</details>

<details>
<summary>Welches Problem löst statische Typisierung, das reines JavaScript nicht löst?</summary>

Typfehler (z. B. eine Zahl an eine Funktion übergeben, die einen String erwartet) werden bereits beim Kompilieren erkannt, statt erst zur Laufzeit oder gar nicht.

</details>

<details>
<summary>Warum lohnt sich TypeScript besonders für ein wachsendes Backend-Projekt wie TeamBoard?</summary>

Je mehr Module (REST, GraphQL, Auth) auf denselben Datenstrukturen (`Ticket`, `Status`) aufbauen, desto wertvoller ist eine verbindliche, geprüfte Typdefinition dafür.

</details>

---

## ECMAScript-Entwicklung kurz eingeordnet

- JavaScript folgt dem ECMAScript-Standard, der jährlich weiterentwickelt wird (z. B. ES2015/ES6 brachte `class`, `let`/`const`, Arrow Functions).
- TypeScript baut auf dem jeweils aktuellen ECMAScript-Standard auf und ergänzt Typen, die beim Kompilieren entfernt werden.

**Grenze:** TypeScript ändert nicht, wie JavaScript zur Laufzeit funktioniert - es prüft nur vorher, ob der Code in sich konsistent ist.

---

## Ein Skript migrieren

```js
// vorher: add.js
function add(a, b) {
  return a + b;
}
add(2, "3"); // liefert "23", kein Fehler
```

```ts
// nachher: add.ts
function add(a: number, b: number): number {
  return a + b;
}
add(2, "3"); // Kompilierfehler: Argument of type 'string' is not assignable to type 'number'
```

---

## Was TypeScript nicht ist

- Kein anderer Laufzeit-Interpreter - am Ende läuft immer JavaScript.
- Kein Ersatz für Tests - Typfehler und Logikfehler sind unterschiedliche Fehlerklassen.

---

## Checkpoint

Ein einfaches JS-Skript wurde nach TypeScript migriert; ein absichtlicher Typfehler wurde vom Compiler erkannt.

Weiter geht es mit Lab 6.2: `tsconfig.json`-Setup.
