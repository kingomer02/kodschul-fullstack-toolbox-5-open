# Modul 14: REST-APIs mit Express

## Lab 14.4 - Vertiefung: Ressourcen schneiden und HTTP-Methoden richtig einsetzen

---

## Lab-Ziel

Die API aus Lab 14.2 funktioniert, ist aber eher "RPC über HTTP": Für jede Aktion gibt es eine eigene URL (`/assign`, `/status`). Du ergänzt die fehlenden Standardoperationen auf der Ressource selbst und triffst dabei bewusst Designentscheidungen.

**Leitfragen:**

<details>
<summary>Was ist in REST eigentlich die "Ressource" - und was die "Aktion"?</summary>

Die Ressource ist das Ding (`/tickets/t-1`), die Aktion steckt in der HTTP-Methode (`GET`, `PATCH`, `DELETE`). `PATCH /tickets/t-1/assign` versteckt die Aktion im Pfad. Das ist nicht verboten, aber jede neue Feldänderung bräuchte eine neue URL.

</details>

<details>
<summary>Soll ein generisches Update auch den Status ändern dürfen?</summary>

Das ist die eigentliche Designfrage dieses Labs. Der Status folgt einer Fachregel (nur einen Schritt vorwärts, siehe `moveToNextStatus`). Ein freies Feld-Update würde diese Regel umgehen: `To Do` direkt auf `Done`. Deshalb bleibt der Statuswechsel eine eigene Aktion. **Fachregeln gehören nicht in ein generisches Update.**

</details>

---

## Die Methoden im Überblick

| Methode | Bedeutung | Idempotent? | Typische Antwort |
|---|---|---|---|
| `GET` | lesen | ja | `200` |
| `POST` | neu anlegen (Server vergibt die ID) | **nein** | `201` + `Location`-Header |
| `PUT` | Ressource **komplett ersetzen** | ja | `200` oder `204` |
| `PATCH` | **einzelne Felder** ändern | nicht garantiert | `200` |
| `DELETE` | löschen | ja | `204` |

**Idempotent** heißt: Zehnmal dieselbe Anfrage hinterlässt denselben **Serverzustand** wie einmal. Das heißt nicht, dass die Antwort gleich bleibt: Das zweite `DELETE` liefert `404`, der Zustand ("Ticket ist weg") ist aber derselbe.

Warum das wichtig ist: Bei Netzwerkfehlern wiederholen Clients, Proxys und Load Balancer Anfragen. Ein wiederholtes `DELETE` ist harmlos, ein wiederholtes `POST` erzeugt ein zweites Ticket.

---

## `201` und der `Location`-Header

Nach einem `POST` sagt der `Location`-Header, **wo** die neue Ressource liegt. Express setzt ihn mit `res.location(...)`. Der Client muss die URL dann nicht selbst zusammenbauen.

## `204 No Content`

Nach erfolgreichem `DELETE` gibt es nichts zurückzugeben. `res.status(204).end()` - ohne Body.

---

## Brücke zu dem, was du kennst

In Spring entspricht das `@PatchMapping("/{id}")` und `@DeleteMapping("/{id}")`, `ResponseEntity.created(uri)` setzt den `Location`-Header. In FastAPI `@app.patch(...)` mit einem Pydantic-Modell, dessen Felder alle optional sind.

---

## Checkpoint

`PATCH /tickets/:id` ändert Titel, Beschreibung oder Zuständigen, lehnt aber `status` ab. `DELETE /tickets/:id` liefert `204`, ein zweites Mal `404`. `POST /tickets` liefert einen `Location`-Header.

## Projektbezug

`PATCH /tickets/:id/assign` und `PATCH /tickets/:id/status` bleiben bestehen: Die Transfer-Übungen und das React-Frontend am Freitag nutzen sie.
