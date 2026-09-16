# Lab 7.2 - Übung: Interfaces

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - generische Übung mit `Person`; das `Ticket`-Interface folgt in Lab 7.3.

## Ausgangslage

Ein lauffähiges TypeScript-Setup existiert (Modul 6).

## Aufgaben

1. Definiere ein `interface Person` mit `name: string`, `age: number` und optionalem `email?: string`.
2. Lege zwei Objekte vom Typ `Person` an: eines mit, eines ohne `email`.
3. Lege absichtlich ein drittes, unvollständiges Objekt an (z. B. ohne `age`) und beobachte den Kompilierfehler.
4. Ergänze eine Funktion `greet(person: Person): string`, die einen Begrüßungstext zurückgibt, und rufe sie mit beiden gültigen Objekten auf.

## Checkpoint

- `npx tsc people.ts --noEmit` meldet für das unvollständige Objekt (Aufgabe 3) einen klaren Fehler.
- Nach Entfernen/Korrektur des unvollständigen Objekts kompiliert die Datei fehlerfrei.

## Abschlusskriterien

- `greet()` funktioniert sowohl mit als auch ohne `email` im übergebenen Objekt.

## Fallback

Bei Unsicherheit über optionale Eigenschaften: zunächst alle Eigenschaften verpflichtend machen, den Unterschied zu `?` anschließend gezielt an einem einzigen Beispiel nachvollziehen.
