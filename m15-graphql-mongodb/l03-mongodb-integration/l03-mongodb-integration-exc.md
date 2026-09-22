# Lab 15.3 - Übung: MongoDB-Integration für TeamBoard

**Dauer:** ca. 60 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - ersetzt die In-Memory-Speicherung durch echte MongoDB-Persistenz und ergänzt GraphQL.

## Ausgangslage

- Express-REST-API (Modul 14) läuft containerisiert; `docker-compose.yml` stellt `MONGO_URL` bereit, wird aber noch nicht genutzt.

## Aufgaben

> **Paketwahl:** `apollo-server` und `apollo-server-express` (Apollo Server v2/v3) sind seit November 2023 abgekündigt und erhalten keine Sicherheitsupdates mehr. Nehmt **`@apollo/server`** zusammen mit **`@as-integrations/express4`**. Die Importe entsprechend: `import { ApolloServer } from "@apollo/server"`, `import { expressMiddleware } from "@as-integrations/express4"`; `gql` kommt aus `graphql-tag`.

1. Installiere im `backend/`-Ordner `mongodb`, `@apollo/server`, `@as-integrations/express4`, `graphql` und `graphql-tag`.
2. Stelle `TicketRepository` auf eine echte MongoDB-Collection um (`connect`, `add`, `findById`, `getAll` als `async`-Methoden, siehe Theorieteil).
3. Passe alle Aufrufstellen in `index.ts` an, damit sie die neuen `async`-Methoden korrekt mit `await` verwenden (inkl. der Routen aus Modul 14).
4. Erstelle `backend/src/graphql/schema.ts` mit `typeDefs` (Typ `Ticket`, Query `tickets`, Mutation `createTicket`) und passenden Resolvern.
5. Hänge einen Apollo-Server unter `/graphql` in die bestehende Express-App aus Modul 14 ein.
6. Starte alles über `docker compose up -d --build` und teste im GraphQL-Playground (`http://localhost:3000/graphql`) die `tickets`-Query und die `createTicket`-Mutation.
7. Prüfe die Persistenz: `docker compose restart backend`, dann erneut `tickets`-Query - die zuvor erstellten Tickets müssen weiterhin vorhanden sein.
8. Committe die Änderungen.

## Checkpoint

- Die `tickets`-Query im Playground liefert dieselben Tickets wie `GET /tickets`.
- Nach `docker compose restart backend` sind alle zuvor per `createTicket` angelegten Tickets weiterhin vorhanden.

## Abschlusskriterien

- REST-Endpunkte aus Modul 14 funktionieren unverändert weiter (jetzt gegen MongoDB statt In-Memory).
- Der Konsolen-Log beim Start bestätigt eine erfolgreiche Verbindung, bevor der Server auf Anfragen wartet.

## Fallback

Falls die Verbindung zu MongoDB beim ersten Start fehlschlägt (Container-Startreihenfolge): `docker compose up -d --build` erneut ausführen - `depends_on` sorgt für einen späteren, erfolgreichen Start.
