# Modul 15: GraphQL und MongoDB

## Lab 15.4 - Vertiefung: async-Fehler abfangen und Abfragen in die Datenbank verlegen

> Setzt die REST-Vertiefung 14.4-14.7 voraus.

---

## Lab-Ziel

Nach Lab 15.3 läuft alles gegen MongoDB - bis zum ersten Fehler: Ein `404` oder `422` beendet den ganzen Server. Du findest die Ursache, behebst sie an einer Stelle und verlegst danach Filter, Sortierung und Blättern aus dem Arbeitsspeicher in die Datenbank.

**Leitfragen:**

<details>
<summary>Warum stürzt der Server ab, obwohl es eine Fehler-Middleware gibt?</summary>

Express 4 fängt nur Fehler, die **synchron** geworfen werden. Ein `async`-Handler wirft nicht, er gibt eine **abgelehnte Promise** zurück. Express 4 schaut sich den Rückgabewert nicht an, die Ablehnung bleibt unbehandelt - und Node beendet seit Version 15 bei unbehandelten Ablehnungen den Prozess. Express 5 prüft den Rückgabewert und leitet die Ablehnung weiter; im Kurs bleiben wir bei Express 4.

</details>

<details>
<summary>Warum reicht es nicht, im Repository `getAll()` aufzurufen und dann zu filtern?</summary>

Bei drei Tickets merkt man nichts. Bei 100.000 lädt jede Anfrage alle 100.000 Dokumente über das Netzwerk in den Speicher, um dann 20 davon zu verschicken. Die Datenbank kann filtern, sortieren und blättern, bevor irgendetwas übertragen wird - und sie kann dafür Indizes nutzen.

</details>

---

## Der Wrapper

```ts
// Idee - die genaue Typisierung ist Teil der Übung
function asyncHandler(handler) {
  return (req, res, next) => {
    handler(req, res, next).catch(next);   // Ablehnung an die Fehler-Middleware
  };
}

router.get("/:id", asyncHandler(async (req, res) => { ... }));
```

---

## MongoDB-Abfragen im Überblick

| In Lab 14.7 (Array) | MongoDB-Treiber |
|---|---|
| `.filter(t => t.status === "Done")` | `collection.find({ status: "Done" })` |
| `.sort((a, b) => a.title.localeCompare(b.title))` | `.sort({ title: 1 })` (`-1` = absteigend) |
| `.slice(offset, offset + limit)` | `.skip(offset).limit(limit)` |
| `result.length` vor dem Schneiden | `collection.countDocuments(filter)` |

**Sortierung und Groß-/Kleinschreibung:** `localeCompare` sortiert wie ein Wörterbuch. MongoDB sortiert standardmäßig nach Zeichencode - dann stehen alle Großbuchstaben vor allen Kleinbuchstaben. Mit `.collation({ locale: "de" })` sortiert MongoDB wie ein Mensch.

**Indizes:** `createIndex({ id: 1 }, { unique: true })` beschleunigt die Suche nach unserer `id` und verhindert doppelte IDs. MongoDB kennt nur `_id` als eindeutigen Schlüssel - dass unser Feld `id` eindeutig sein soll, weiß die Datenbank nicht von selbst.

---

## Brücke zu dem, was du kennst

- Der Absturz entspricht einer unbehandelten Exception in einem eigenen Thread, die niemand fängt - nur dass Node daraufhin den ganzen Prozess beendet.
- Die Verlagerung in die Datenbank ist dasselbe wie der Schritt von `findAll().stream().filter(...)` zu einer Spring-Data-Methode `findByStatus(status, pageable)`.

---

## Checkpoint

`404` und `422` kommen wieder als JSON-Antwort, der Server läuft weiter. `GET /tickets?sort=title` sortiert unabhängig von Groß- und Kleinschreibung, `X-Total-Count` stimmt weiterhin.

## Projektbezug

Route, Schema und Service bleiben unverändert - nur `TicketRepository.find` wird ausgetauscht. Das ist die Trennung aus Modul 8, diesmal ohne Einschränkung.
