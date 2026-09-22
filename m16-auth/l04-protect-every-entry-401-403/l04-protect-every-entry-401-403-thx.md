# Modul 16: Authentifizierung

## Lab 16.4 - Vertiefung: Jeden Eingang schützen, 401 von 403 trennen

---

## Lab-Ziel

Nach Lab 16.3 sieht die API geschützt aus: `GET /tickets` ohne Token liefert `401`. Über `/graphql` lässt sich aber weiterhin alles lesen **und schreiben**. Du schließt diese Lücke und lernst den Unterschied zwischen "wer bist du?" (Authentifizierung) und "was darfst du?" (Autorisierung).

**Leitfragen:**

<details>
<summary>Warum ist `/graphql` nach Lab 16.3 offen?</summary>

`app.use("/tickets", requireAuth)` schützt einen **Pfad**, nicht die Daten. GraphQL erreicht dieselben Tickets über einen anderen Pfad. Die Lehre: Schutz gehört an **jeden** Eingang - oder tiefer, an die Stelle, an der auf die Daten zugegriffen wird.

</details>

<details>
<summary>`401` oder `403`?</summary>

- `401 Unauthorized` (trotz des Namens): **Wir wissen nicht, wer du bist.** Kein Token, kaputter Token, abgelaufener Token.
- `403 Forbidden`: **Wir wissen, wer du bist - und du darfst das nicht.**

Wer bei fehlender Berechtigung `401` schickt, verleitet den Client dazu, sich neu anzumelden, obwohl das nichts ändert.

</details>

---

## Zwei Wege, GraphQL zu schützen

**Weg A - Middleware vor den Pfad:** `app.use("/graphql", requireAuth, ...)`. Einfach, aber grob: Auch die Apollo-Oberfläche (`GET /graphql` im Browser) braucht dann einen Token und lädt nicht mehr.

**Weg B - Kontext und Prüfung im Resolver:** Apollo ruft bei jeder Anfrage eine `context`-Funktion auf. Dort liest man den Token aus und gibt den Benutzer an alle Resolver weiter. Jeder Resolver entscheidet selbst. Feiner, und die Oberfläche bleibt erreichbar.

```ts
app.use("/graphql", expressMiddleware(apollo, {
  context: async ({ req }) => ({ username: /* aus dem Token */ }),
}));

// im Resolver: dritter Parameter ist der Kontext
tickets: (_parent, _args, ctx) => { /* ctx.username prüfen */ }
```

Ein Fehler mit `extensions: { code: "UNAUTHENTICATED", http: { status: 401 } }` sorgt dafür, dass Apollo auch den HTTP-Status auf `401` setzt statt `200`.

---

## Wer hat es angelegt?

Um "nur die Erstellerin darf löschen" prüfen zu können, muss das Ticket wissen, wer es angelegt hat. Das Feld setzt **der Server** aus dem Token - nie der Client. Schickt ein Client `createdBy` mit, wird das abgelehnt (das strikte Schema aus Lab 14.6 erledigt das schon).

Damit die Routen wissen, wer anfragt, legt `requireAuth` den Benutzernamen in `res.locals` ab. `res.locals` ist ein Objekt, das Express pro Anfrage bereitstellt, genau für solche Daten.

---

## Brücke zu dem, was du kennst

Spring Security trennt dasselbe: `AuthenticationEntryPoint` liefert `401`, `AccessDeniedHandler` liefert `403`. `res.locals.username` entspricht `SecurityContextHolder.getContext().getAuthentication()`.

---

## Checkpoint

`POST /graphql` ohne Token → `401`, mit Token → `200`. Die Apollo-Oberfläche lädt weiterhin. Ein fremdes Ticket löschen → `403`, ein eigenes → `204`.

## Projektbezug

Das React-Frontend am Freitag schickt den Token bereits bei jeder Anfrage mit - es merkt von dieser Änderung nichts.
