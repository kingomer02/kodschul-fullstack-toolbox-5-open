# Modul 14: REST-APIs mit Express

## Lab 14.1 - Ressourcen, HTTP-Methoden und Statuscodes

---

## Lab-Ziel

Du kennst die REST-Grundregeln (Ressourcen, HTTP-Methoden, Statuscodes) und kannst eine einfache Express-Ressource aus dem Stand implementieren.

**Leitfragen:**

<details>
<summary>Was unterscheidet `PUT` von `PATCH`?</summary>

`PUT` ersetzt eine Ressource vollständig; `PATCH` ändert nur die übergebenen Felder, der Rest bleibt unverändert.

</details>

<details>
<summary>Welcher Statuscode passt zu "Ressource erfolgreich erstellt"?</summary>

`201 Created` - im Unterschied zu `200 OK` für eine bereits bestehende, erfolgreich gelieferte Ressource.

</details>

<details>
<summary>Welcher Statuscode passt zu "Ressource mit dieser ID existiert nicht"?</summary>

`404 Not Found`.

</details>

---

## REST-Grundregeln

| HTTP-Methode | Bedeutung                          | Beispiel            |
| ------------ | ---------------------------------- | ------------------- |
| `GET`        | Ressource(n) lesen, keine Änderung | `GET /items`        |
| `POST`       | neue Ressource anlegen             | `POST /items`       |
| `PATCH`      | Teil einer Ressource ändern        | `PATCH /items/:id`  |
| `DELETE`     | Ressource entfernen                | `DELETE /items/:id` |

| Statuscode | Bedeutung                              |
| ---------- | -------------------------------------- |
| `200`      | Erfolg (lesend/ändernd)                |
| `201`      | Ressource erfolgreich erstellt         |
| `400`      | fehlerhafte Anfrage (z. B. Feld fehlt) |
| `404`      | Ressource nicht gefunden               |

---

## Minimalbeispiel: `/items`

```ts
// sample-api/src/server.ts
import express from "express";

const app = express();
app.use(express.json());

interface Item {
  id: string;
  name: string;
}

const items: Item[] = [];

app.get("/items", (req, res) => {
  res.status(200).json(items);
});

app.post("/items", (req, res) => {
  const { name } = req.body;
  if (!name) {
    return res.status(400).json({ error: "name is required" });
  }
  const item: Item = { id: String(items.length + 1), name };
  items.push(item);
  res.status(201).json(item);
});

app.listen(3000, () => console.log("Sample API listening on port 3000"));
```

---

## Checkpoint

`curl http://localhost:3000/items` liefert `[]`; nach einem `POST` mit `{"name": "test"}` liefert ein erneutes `GET` das neue Element mit Status `201` bei der Erstellung.

Weiter geht es mit Lab 14.2: die Ticket-REST-API für TeamBoard.
