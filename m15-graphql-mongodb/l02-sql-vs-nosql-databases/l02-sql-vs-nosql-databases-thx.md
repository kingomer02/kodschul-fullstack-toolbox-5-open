# Modul 15: GraphQL und MongoDB

## Lab 15.2 - SQL versus NoSQL: Ticket-Daten modellieren

---

## Lab-Ziel

Du kannst dieselben Ticket-Daten sowohl als relationales (SQL-)Tabellenmodell als auch als dokumentenbasiertes (MongoDB-)Modell entwerfen und die Vor- und Nachteile für TeamBoard einschätzen.

**Leitfragen:**

<details>
<summary>Warum passt ein Dokumentenmodell (MongoDB) gut zu einem `Ticket` mit den Feldern `title`, `description`, `assignee`, `status`?</summary>

Ein Ticket ist ein in sich geschlossenes Objekt ohne komplexe Beziehungen zu anderen Tabellen - es lässt sich direkt als ein JSON-ähnliches Dokument speichern, ohne es über mehrere Tabellen zu verteilen.

</details>

<details>
<summary>Wann wäre ein relationales Modell (SQL) für TeamBoard klar im Vorteil?</summary>

Sobald feste Beziehungen mit strikter Konsistenz nötig werden, z. B. ein `assignee`, der zwingend auf einen existierenden Nutzer in einer separaten `users`-Tabelle verweisen muss (referenzielle Integrität).

</details>

---

## Ticket als SQL-Tabelle

```sql
CREATE TABLE tickets (
  id UUID PRIMARY KEY,
  title VARCHAR(255) NOT NULL,
  description TEXT,
  assignee VARCHAR(255),
  status VARCHAR(20) NOT NULL DEFAULT 'To Do'
);
```

- Feste Spalten, feste Typen - eine Änderung der Struktur (neue Spalte) betrifft sofort alle Zeilen.

## Ticket als MongoDB-Dokument

```json
{
  "_id": "t-1",
  "title": "Login-Formular bauen",
  "description": "E-Mail und Passwort-Feld",
  "assignee": "Alex",
  "status": "To Do"
}
```

- Kein festes Schema auf Datenbankebene - unterschiedliche Tickets könnten theoretisch unterschiedliche Felder haben (in der Praxis über die Anwendung, z. B. TypeScript-Interfaces, trotzdem konsistent gehalten).

---

## Vergleich

| Kriterium                 | SQL (relational)               | MongoDB (Dokument)                      |
| ------------------------- | ------------------------------ | --------------------------------------- |
| Schema                    | fest, beim Anlegen der Tabelle | flexibel, pro Dokument                  |
| Beziehungen               | stark (Foreign Keys, JOINs)    | schwach (eingebettet oder referenziert) |
| Passt zu TeamBoard-Ticket | möglich, aber mit fixem Schema | sehr direkt (Ticket = 1 Dokument)       |

**Grenze:** Dieser Vergleich ist bewusst vereinfacht - beide Datenbankarten unterstützen inzwischen Mischformen (z. B. JSON-Spalten in SQL, Schema-Validierung in MongoDB).

---

## Checkpoint

Du kannst für ein gegebenes Datenmodell (z. B. "Tickets mit Kommentaren") begründen, ob ein relationales oder dokumentenbasiertes Modell besser passt.

## Projektbezug

TeamBoard nutzt MongoDB, weil Tickets als in sich geschlossene Dokumente ohne komplexe Beziehungen gut passen. Weiter geht es mit Lab 15.3: die tatsächliche MongoDB-Integration.
