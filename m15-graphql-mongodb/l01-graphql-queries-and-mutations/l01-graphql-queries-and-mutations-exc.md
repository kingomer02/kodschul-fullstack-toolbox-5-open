# Lab 15.1 - Übung: GraphQL Queries und Mutations

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - eigenständiges Beispielprojekt.

## Vorbereitung

- Ein leerer Ordner `sample-graphql/` mit `npm init -y` und `npm install @apollo/server graphql graphql-tag` liegt bereit.

## Aufgaben

1. Erstelle `sample-graphql/src/server.ts` mit einem `Book`-Typ (`id`, `title`), einer `books`-Query und einer `addBook`-Mutation.
2. Starte den Server (`ts-node` oder kompiliert mit `tsc` + `node`).
3. Öffne den angezeigten Playground-Link im Browser und führe eine `books`-Query aus.
4. Führe eine `addBook`-Mutation mit einem eigenen Titel aus und bestätige per erneuter `books`-Query, dass das Buch übernommen wurde.

## Checkpoint

- Die `books`-Query liefert vor der Mutation genau ein Buch, danach zwei.

## Abschlusskriterien

- Du kannst im Playground selbstständig eine Query so anpassen, dass nur das Feld `title` (ohne `id`) zurückgegeben wird, und erklären, warum das bei REST so nicht möglich wäre.

## Fallback

Falls der Standalone-Server Versionskonflikte verursacht: `@apollo/server` zusammen mit `@as-integrations/express4` und einem minimalen Express-Server verwenden (wird in Lab 15.3 ohnehin eingesetzt).
