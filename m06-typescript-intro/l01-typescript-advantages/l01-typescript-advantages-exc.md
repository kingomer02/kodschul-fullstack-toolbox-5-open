# Lab 6.1 - Übung: ECMAScript-Entwicklung und Vorteile von TypeScript

**Dauer:** ca. 15 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - generische Übung an einem eigenständigen Skript.

## Ausgangslage

TypeScript ist als `devDependency` im `backend/`-Projekt installiert (Lab 5.2).

## Aufgaben

1. Schreibe ein kleines JavaScript-Skript `discount.js`, das einen Preis und einen Rabatt-Prozentsatz entgegennimmt und den reduzierten Preis zurückgibt.
2. Rufe die Funktion einmal absichtlich mit einem String statt einer Zahl auf und beobachte das Ergebnis mit `node discount.js`.
3. Kopiere das Skript nach `discount.ts`, ergänze Parameter- und Rückgabetypen.
4. Kompiliere mit `npx tsc discount.ts` und beobachte den Fehler bei der falschen Aufrufart - korrigiere den Aufruf.

## Checkpoint

- `discount.ts` hat typisierte Parameter und einen typisierten Rückgabewert.
- `npx tsc discount.ts` erzeugt bei korrektem Aufruf keine Fehlermeldung.

## Abschlusskriterien

- Der ursprüngliche Fehlerfall (String statt Zahl) wird vom Compiler klar benannt, bevor der Code läuft.

## Fallback

Ohne lokale `tsc`-Installation: den TypeScript Playground (offiziell, im Browser) für diese kurze Übung verwenden.
