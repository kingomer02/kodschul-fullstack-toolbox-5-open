# Lab 7.2 - Lösung: Interfaces

## Aufgabe 1-2: Interface und gültige Objekte

```ts
// people.ts
interface Person {
  name: string;
  age: number;
  email?: string;
}

const alex: Person = { name: "Alex", age: 29 };
const sam: Person = { name: "Sam", age: 31, email: "sam@example.com" };
```

## Aufgabe 3: Absichtlich unvollständiges Objekt

```ts
const invalid: Person = { name: "Jo" };
// Fehler: Property 'age' is missing in type '{ name: string; }' but required in type 'Person'.
```

Für die Abschlusskriterien wird diese Zeile nach dem Beobachten wieder entfernt oder auskommentiert.

## Aufgabe 4: Funktion mit `Person`-Parameter

```ts
function greet(person: Person): string {
  return person.email
    ? `Hallo ${person.name} (${person.email})`
    : `Hallo ${person.name}`;
}

console.log(greet(alex)); // Hallo Alex
console.log(greet(sam)); // Hallo Sam (sam@example.com)
```

## Grenzen

Dieses `Person`-Interface dient nur der Übung - das für TeamBoard tatsächlich verwendete Modell ist `Ticket` aus Lab 7.3.
