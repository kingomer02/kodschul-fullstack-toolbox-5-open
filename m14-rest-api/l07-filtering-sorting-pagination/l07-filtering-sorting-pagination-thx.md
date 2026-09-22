# Modul 14: REST-APIs mit Express

## Lab 14.7 - Vertiefung: Filtern, Sortieren, Paginieren

---

## Lab-Ziel

`GET /tickets` liefert immer alles. Bei drei Tickets egal, bei dreitausend nicht. Du ergänzt Filter, Sortierung und Blättern über **Query-Parameter** und prüfst sie mit demselben Werkzeug wie in Lab 14.6.

**Leitfragen:**

<details>
<summary>Warum Query-Parameter und nicht eigene URLs wie `/tickets/done`?</summary>

Die Ressource bleibt dieselbe - die Ticketliste. Filter und Sortierung sind nur eine **Sicht** darauf. Sie lassen sich frei kombinieren (`?status=Done&assignee=Alex&sort=title`), eigene URLs könnten das nicht.

</details>

<details>
<summary>Woher weiß der Client, wie viele Seiten es gibt?</summary>

Er braucht die **Gesamtzahl der Treffer vor dem Blättern**. Zwei verbreitete Wege: ein Umschlag-Objekt (`{ items: [...], total: 42 }`) oder ein Header (`X-Total-Count: 42`) bei unverändertem Array. Der Header hat einen Vorteil: Bestehende Clients, die ein Array erwarten, laufen weiter.

</details>

---

## Query-Parameter sind immer Text

```text
GET /tickets?limit=10
req.query.limit  →  "10"     (string, nicht number)
```

`z.coerce.number()` wandelt vor der Prüfung um: `"10"` wird zu `10`, `"abc"` zu `NaN` und fällt durch. Bei `z.strictObject` fällt auch ein Tippfehler im Parameternamen auf (`?stauts=Done`), statt still ignoriert zu werden.

---

## Paginierung: `limit` und `offset`

```text
?limit=2&offset=0   → Treffer 1-2
?limit=2&offset=2   → Treffer 3-4
```

Die Reihenfolge ist nur mit einer **festen Sortierung** stabil. Ohne `sort` kann sich die Reihenfolge zwischen zwei Aufrufen ändern, und ein Eintrag erscheint auf zwei Seiten oder auf keiner.

**Wo gehört die Logik hin?** Ins Repository. Dort sitzt heute ein Array, ab Modul 15 MongoDB. Die Route übergibt nur die geprüfte Anfrage und bekommt `{ items, total }` zurück - wie gefiltert wird, ist Sache des Repositorys.

---

## Brücke zu dem, was du kennst

Spring Data: `Pageable` mit `page`, `size`, `sort` und `Page<T>` mit `getTotalElements()`. Dieselbe Idee, hier von Hand.

---

## Checkpoint

Filter, Sortierung und Blättern lassen sich kombinieren, `X-Total-Count` nennt die Treffer vor dem Blättern, ungültige Parameter liefern `422`.

## Projektbezug

In Lab 15.4 wandert genau diese Repository-Methode auf MongoDB (`find`, `sort`, `skip`, `limit`, `countDocuments`) - Route und Schema bleiben unverändert.
