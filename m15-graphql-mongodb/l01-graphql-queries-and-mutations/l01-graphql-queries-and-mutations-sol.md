# Lab 15.1 - Lösung: GraphQL Queries und Mutations

## Aufgabe 1: `server.ts`

Siehe vollständigen Code im Theorieteil (Lab 15.1, Abschnitt "Minimalbeispiel: Bücher-Schema").

## Aufgabe 2: Starten

```bash
cd sample-graphql
npx ts-node src/server.ts
# Sample GraphQL API at http://localhost:4000/
```

## Aufgabe 3-4: Abfragen im Playground

```graphql
query {
  books {
    id
    title
  }
}
# { "data": { "books": [{ "id": "1", "title": "Clean Code" }] } }

mutation {
  addBook(title: "Refactoring") {
    id
    title
  }
}
# { "data": { "addBook": { "id": "2", "title": "Refactoring" } } }

query {
  books {
    title
  }
}
# { "data": { "books": [{ "title": "Clean Code" }, { "title": "Refactoring" }] } }
```

## Grenzen

Die Daten leben nur im Arbeitsspeicher; ein Serverneustart setzt `books` auf den Startzustand zurück.
