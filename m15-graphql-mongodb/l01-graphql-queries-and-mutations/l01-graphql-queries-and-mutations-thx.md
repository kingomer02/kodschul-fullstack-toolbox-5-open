# Modul 15: GraphQL und MongoDB

## Lab 15.1 - GraphQL: Queries und Mutations

---

## Lab-Ziel

Du kannst ein einfaches GraphQL-Schema mit Query und Mutation auf Beispieldaten erstellen und über den GraphQL-Playground abfragen.

**Leitfragen:**

<details>
<summary>Was ist der Hauptunterschied zwischen einer REST-Anfrage und einer GraphQL-Query bezüglich der zurückgegebenen Felder?</summary>

Bei REST bestimmt der Server, welche Felder eine Antwort enthält; bei GraphQL bestimmt die Anfrage selbst, welche Felder zurückgegeben werden.

</details>

<details>
<summary>Was ist der Unterschied zwischen einer GraphQL-`query` und einer `mutation`?</summary>

`query` liest nur Daten, ohne sie zu verändern; `mutation` verändert Daten (anlegen, ändern, löschen) - vergleichbar mit `GET` versus `POST`/`PATCH` in REST.

</details>

---

## Minimalbeispiel: Bücher-Schema

```ts
// sample-graphql/src/server.ts
import { ApolloServer, gql } from "apollo-server";

interface Book {
  id: string;
  title: string;
}

const books: Book[] = [{ id: "1", title: "Clean Code" }];

const typeDefs = gql`
  type Book {
    id: ID!
    title: String!
  }

  type Query {
    books: [Book!]!
  }

  type Mutation {
    addBook(title: String!): Book!
  }
`;

const resolvers = {
  Query: {
    books: () => books,
  },
  Mutation: {
    addBook: (_: unknown, args: { title: string }) => {
      const book: Book = { id: String(books.length + 1), title: args.title };
      books.push(book);
      return book;
    },
  },
};

const server = new ApolloServer({ typeDefs, resolvers });
server.listen().then(({ url }) => console.log(`Sample GraphQL API at ${url}`));
```

---

## Abfragen im Playground

```graphql
query {
  books {
    id
    title
  }
}

mutation {
  addBook(title: "Refactoring") {
    id
    title
  }
}
```

---

## Checkpoint

Die `books`-Query liefert das Startbuch; die `addBook`-Mutation liefert das neu angelegte Buch mit generierter `id`, und eine erneute `books`-Query enthält beide Bücher.

Weiter geht es mit Lab 15.2: SQL versus NoSQL.
