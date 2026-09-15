# Ticket Contract

This is the stable shape of a TeamBoard ticket, used consistently from Module 7 (typed models) through the React frontend (Module 19). Do not change these field names in your own implementation - later labs and their solutions assume this exact contract.

## Data Shape

```ts
interface Ticket {
  id: string;
  title: string;
  description: string;
  assignee: string;
  status: "To Do" | "In Progress" | "Done";
}
```

## REST Endpoints (introduced in m14)

| Method  | Path           | Purpose                       |
| ------- | -------------- | ----------------------------- |
| `GET`   | `/tickets`     | list all tickets              |
| `POST`  | `/tickets`     | create a ticket               |
| `PATCH` | `/tickets/:id` | update assignee and/or status |

## GraphQL Shape (introduced in m15)

```graphql
type Ticket {
  id: ID!
  title: String!
  description: String!
  assignee: String!
  status: String!
}

type Query {
  tickets: [Ticket!]!
}

type Mutation {
  createTicket(title: String!, description: String!): Ticket!
  updateTicket(id: ID!, assignee: String, status: String): Ticket!
}
```

## Authentication (introduced in m16)

All `/tickets` routes require a valid `Authorization: Bearer <jwt>` header once Module 16 is complete. Before that module, routes are open.
