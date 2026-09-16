# Modul 14: REST-APIs mit Express

## Lab 14.3 - Die API im Container testen

---

## Lab-Ziel

Du verifizierst die neue REST-API nicht nur lokal, sondern containerisiert über `docker-compose.yml`, und passt die Compose-Konfiguration für eine erreichbare Portfreigabe an.

**Leitfragen:**

<details>
<summary>Warum reicht ein containerisierter Serverstart allein nicht - was fehlt noch in `docker-compose.yml`?</summary>

Ohne eine `ports`-Zuordnung ist der im Container laufende Port zwar aktiv, aber vom Host-Rechner aus nicht erreichbar.

</details>

<details>
<summary>Warum bleibt der Backend-Container jetzt dauerhaft im Status "running", statt sich sofort zu beenden (Verhalten aus Modul 11-13)?</summary>

`app.listen(...)` blockiert den Node-Prozess dauerhaft, solange keine Beendigung erfolgt - im Gegensatz zum vorherigen Skript, das nach dem letzten `console.log` durchlief und endete.

</details>

---

## Portfreigabe ergänzen

```yaml
# docker-compose.yml (Ausschnitt, ergänzt)
services:
  backend:
    build: ./backend
    ports:
      - "3000:3000"
    depends_on:
      - mongo
    environment:
      MONGO_URL: mongodb://mongo:27017/teamboard
```

- `"3000:3000"`: Host-Port 3000 wird auf Container-Port 3000 weitergeleitet.

---

## Testen mit curl/Postman gegen den Container

```bash
docker compose up -d --build
curl http://localhost:3000/tickets
docker compose logs backend
```

- `docker compose logs backend` zeigt `TeamBoard backend listening on port 3000` statt des früheren einmaligen Konsolen-Outputs.
- `docker compose ps` zeigt den `backend`-Service dauerhaft als `running`, nicht mehr als `exited`.

---

## Checkpoint

`curl http://localhost:3000/tickets` liefert vom Container aus dieselbe Antwort wie zuvor lokal; `docker compose ps` zeigt `backend` als dauerhaft laufend.

## Projektbezug

Damit ist die REST-API vollständig containerisiert nutzbar. Modul 15 ergänzt GraphQL und eine echte MongoDB-Anbindung, sodass Tickets einen Server-Neustart überleben.
