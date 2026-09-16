# Lab 7.1 - Lösung: Basistypen und Type Inference

## Aufgabe 1: Basistypen mit Inference

```ts
// basics.ts
let title = "Setup Repo"; // inferred: string
let priority = 1; // inferred: number
let isDone = false; // inferred: boolean
let tags = ["setup", "git"]; // inferred: string[]
```

## Aufgabe 2-3: Absichtlicher Fehler und Korrektur

```ts
priority = "hoch"; // Fehler: Type 'string' is not assignable to type 'number'
```

Korrektur:

```ts
priority = 2;
```

## Aufgabe 4: `unknown` sicher verwenden

```ts
let unknownValue: unknown = "hallo";
unknownValue.toUpperCase(); // Fehler: Object is of type 'unknown'

if (typeof unknownValue === "string") {
  unknownValue.toUpperCase(); // erlaubt, da hier als string verengt
}
```

## Grenzen

`unknown` erzwingt genau diese Prüfung vor Verwendung - `any` würde denselben Aufruf ohne jede Prüfung durchlassen und Laufzeitfehler riskieren.
