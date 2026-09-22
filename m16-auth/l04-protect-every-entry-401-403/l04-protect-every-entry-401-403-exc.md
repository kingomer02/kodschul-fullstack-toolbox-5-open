# Lab 16.4 - Übung: Jeden Eingang schützen, 401 von 403 trennen

**Dauer:** ca. 35 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - GraphQL wird geschützt, Tickets merken sich, wer sie angelegt hat.

## Ausgangslage

- Lab 16.3 inkl. Zusatzaufgabe: `/tickets` ist geschützt, `/graphql` nicht.
- Für das Löschen: `DELETE /tickets/:id` aus Lab 14.4. Ohne die REST-Vertiefung entfallen Aufgabe 4 und 5.

## Aufgaben

1. **Die Lücke beweisen.** Leg **ohne Token** über `/graphql` ein Ticket an und prüfe mit Token über `GET /tickets`, dass es wirklich gespeichert wurde.
2. Probier Weg A aus dem Theorieteil kurz aus und öffne danach `http://localhost:3000/graphql` im Browser. Was fällt auf? Nimm die Änderung wieder zurück.
3. Setze Weg B um: Den Benutzernamen aus dem Token ermitteln (am besten als eigene Funktion, die `requireAuth` mitbenutzt), in den Apollo-Kontext geben und in jedem Resolver prüfen. Ohne Token soll die Antwort `401` sein, nicht `200`.
4. Ticket bekommt ein optionales Feld `createdBy`. Beim Anlegen (REST **und** GraphQL) setzt der Server es aus dem Token.
5. `DELETE /tickets/:id` darf nur, wer das Ticket angelegt hat. Überlege, welcher Statuscode für "angemeldet, aber nicht berechtigt" richtig ist.
6. Teste mit **zwei** registrierten Nutzern: Wer darf was löschen? Was passiert mit den drei Beispieltickets, die niemand angelegt hat?

## Checkpoint

- `POST /graphql` ohne Token → `401` mit `UNAUTHENTICATED`, mit Token → `200`.
- `GET /graphql` im Browser zeigt weiterhin die Apollo-Oberfläche.
- Fremdes Ticket löschen → `403`, eigenes → `204`, ohne Token → `401`.
- `POST /tickets` mit `"createdBy": "jemand"` im Body → `422`.

## Abschlusskriterien

- Du kannst in einem Satz erklären, wann `401` und wann `403` richtig ist.
- Du kannst begründen, warum der Schutz im Resolver feiner ist als der Schutz vor dem Pfad.

## Fallback

Falls die Resolver den Kontext nicht sehen: Der Kontext ist der **dritte** Parameter eines Resolvers - `(parent, args, context)`. Und `new ApolloServer<DeinKontextTyp>(...)` braucht den Typ als Generic, damit TypeScript ihn kennt.
