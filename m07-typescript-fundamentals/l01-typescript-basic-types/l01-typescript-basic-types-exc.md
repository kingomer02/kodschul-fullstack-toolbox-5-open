# Lab 7.1 - Übung: Basistypen und Type Inference

**Dauer:** ca. 15 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - generische Übung, TeamBoard-Typen folgen in Lab 7.3.

## Ausgangslage

Ein lauffähiges TypeScript-Setup (`tsconfig.json`, Lab 6.2) existiert.

## Aufgaben

1. Lege `basics.ts` an und deklariere je eine Variable für `string`, `number`, `boolean` und ein `string[]`, jeweils ohne explizite Typangabe (Inference nutzen).
2. Weise einer der Variablen absichtlich einen falschen Typ zu und beobachte den Kompilierfehler mit `npx tsc basics.ts --noEmit`.
3. Korrigiere den Fehler.
4. Deklariere eine Variable vom Typ `unknown`, weise ihr einen String zu und versuche, direkt `.toUpperCase()` darauf aufzurufen - beobachte den Fehler und löse ihn mit einer `typeof`-Prüfung.

## Checkpoint

- `npx tsc basics.ts --noEmit` läuft ohne Fehler durch.
- Die `unknown`-Variable wird erst nach einer `typeof`-Prüfung als String verwendet.

## Abschlusskriterien

- Mindestens ein selbst verursachter und wieder behobener Typfehler ist nachvollziehbar (z. B. per Kommentar dokumentiert).

## Fallback

Bei Unsicherheit über `unknown`: zunächst mit `any` arbeiten, den Unterschied anschließend anhand der Trainer-Erklärung direkt am Code nachvollziehen.
