# Lab 6.1 - Lösung: ECMAScript-Entwicklung und Vorteile von TypeScript

## Aufgabe 1-2: JavaScript-Version

```js
// discount.js
function discount(price, percent) {
  return price - (price * percent) / 100;
}

console.log(discount(100, "10")); // "NaN" oder unerwartetes Verhalten, kein Fehler beim Ausführen
```

## Aufgabe 3: TypeScript-Version

```ts
// discount.ts
function discount(price: number, percent: number): number {
  return price - (price * percent) / 100;
}

console.log(discount(100, "10"));
```

## Aufgabe 4: Kompilieren und korrigieren

```bash
npx tsc discount.ts
```

Fehler: `Argument of type 'string' is not assignable to parameter of type 'number'.`

Korrektur:

```ts
console.log(discount(100, 10)); // 90
```

## Grenzen

`npx tsc discount.ts` kompiliert hier ohne `tsconfig.json` mit Compiler-Standardeinstellungen - ein projektweites Setup folgt in Lab 6.2.
