# Modul 6: Einführung in TypeScript

## Lab 6.2 - `tsconfig.json`-Setup

---

## Lab-Ziel

Du hast für das TeamBoard-Backend eine `tsconfig.json` eingerichtet, die Node.js als Zielumgebung berücksichtigt.

**Leitfragen:**

<details>
<summary>Was steuert `tsconfig.json`?</summary>

Sie legt fest, wie der TypeScript-Compiler ein Projekt kompiliert: welche Dateien einbezogen werden, welches JS-Ziel erzeugt wird, wie streng geprüft wird.

</details>

<details>
<summary>Was bewirkt die Option `strict: true`?</summary>

Sie aktiviert eine Reihe strenger Prüfungen auf einmal (u. a. `strictNullChecks`, `noImplicitAny`) - Standardempfehlung für neue Projekte.

</details>

<details>
<summary>Warum `outDir`/`rootDir` statt kompilierte Dateien neben den Quelldateien liegen zu lassen?</summary>

Eine klare Trennung von Quellcode (`src/`) und kompiliertem Output (`dist/`) verhindert, dass generierte `.js`-Dateien versehentlich committet oder mit Quelldateien verwechselt werden.

</details>

---

## `tsconfig.json` generieren

```bash
npx tsc --init
```

Erzeugt eine Datei mit vielen auskommentierten Optionen als Ausgangspunkt.

---

## Relevante Optionen für ein Node-Backend

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "commonjs",
    "rootDir": "src",
    "outDir": "dist",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true
  },
  "include": ["src/**/*"]
}
```

| Option             | Bedeutung                                          |
| ------------------ | -------------------------------------------------- |
| `target`           | welche JS-Version erzeugt wird                     |
| `module`           | Modulsystem (hier: `commonjs`, passend zu Node.js) |
| `rootDir`/`outDir` | Quell- vs. Ausgabeordner                           |
| `strict`           | strenge Typprüfung aktiviert                       |

---

## Build-Skript ergänzen

```json
{
  "scripts": {
    "build": "tsc",
    "start": "node dist/index.js"
  }
}
```

---

## Checkpoint

`npm run build` kompiliert `src/` fehlerfrei nach `dist/`; die CI-Pipeline aus Modul 4 kann `npm run build` jetzt echt statt als Platzhalter ausführen.

---

## CI-Pipeline von Platzhaltern auf echten Build umstellen

In Modul 4 enthielt `package.json` nur Platzhalter-Skripte (`"lint": "echo ..."`, `"build": "echo ..."`). Jetzt werden sie durch die echten Skripte aus diesem Lab ersetzt:

```json
{
  "scripts": {
    "lint": "tsc --noEmit",
    "build": "tsc"
  }
}
```

- Die Workflow-Datei `.github/workflows/ci.yml` selbst bleibt unverändert - sie ruft weiterhin nur `npm run lint`/`npm run build` auf.
- Ein Push mit dieser Änderung lässt die Pipeline erstmals echte TypeScript-Fehler erkennen, statt immer grün zu sein.

Weiter geht es mit Modul 7: TypeScript-Grundlagen (Basistypen, Interfaces, Datenmodelle).
