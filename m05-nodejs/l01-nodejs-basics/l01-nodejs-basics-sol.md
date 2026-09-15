# Lab 5.1 - Lösung: Grundlagen und Installation

## Aufgabe 1: Version prüfen

```bash
node --version   # z. B. v20.11.0
npm --version    # z. B. 10.2.4
```

## Aufgabe 2-3: Skript schreiben und ausführen

```js
// hello.js
console.log("Hallo von", "Alex");
console.log("Node-Version:", process.version);
```

```bash
node hello.js
```

## Aufgabe 4: Plattform ergänzen

```js
console.log("Plattform:", process.platform); // z. B. "darwin", "win32", "linux"
```

## Grenzen

`process.version`/`process.platform` sind Node-spezifische globale Objekte - im Browser existieren sie nicht.
