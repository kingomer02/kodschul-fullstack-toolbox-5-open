# Modul 13: Mehrere Services mit Docker Compose verbinden

## Lab 13.2 - `docker-compose.yml` für TeamBoard

---

## Lab-Ziel

Du kannst Backend und MongoDB als zwei zusammengehörige Services in einer `docker-compose.yml` für TeamBoard definieren und ihre Erreichbarkeit prüfen.

**Leitfragen:**

<details>
<summary>Warum reicht für MongoDB das offizielle `mongo`-Image, aber für das Backend ein eigener `build`-Eintrag?</summary>

MongoDB ist eine fertige Standardsoftware ohne TeamBoard-spezifischen Code; das Backend enthält eigenen Code und muss deshalb aus dem eigenen Dockerfile gebaut werden (vgl. Lab 10.3, Aufgabe 4).

</details>

<details>
<summary>Wozu dient ein benanntes Volume wie `mongo-data:` in der Compose-Datei?</summary>

Es sorgt dafür, dass MongoDB-Daten einen Container-Neustart überleben, statt beim Entfernen des Containers verloren zu gehen.

</details>

---

## `docker-compose.yml`

```yaml
# docker-compose.yml (Projekt-Root)
services:
  backend:
    build: ./backend
    depends_on:
      - mongo
    environment:
      MONGO_URL: mongodb://mongo:27017/teamboard

  mongo:
    image: mongo:8
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

- `build: ./backend` baut das in Modul 11/12 entwickelte Backend-Dockerfile.
- `MONGO_URL` zeigt bereits auf den späteren Verbindungsstring (genutzt ab Modul 15) - der Wert wird hier nur bereitgestellt, noch nicht vom Code gelesen.

---

## Starten und Erreichbarkeit prüfen

```bash
docker compose up -d
docker compose ps
docker compose run --rm --entrypoint sh backend -c "getent hosts mongo"
```

Erwartung: `getent hosts mongo` löst den Servicenamen `mongo` auf eine interne IP im Compose-Netzwerk auf - der Beweis, dass beide Services sich erreichen können.

---

## Checkpoint

`docker compose ps` zeigt `mongo` als laufend, `backend` ist nach einem Durchlauf mit `Exited (0)` beendet (erst ab Modul 14 ist es ein Server); `getent hosts mongo` aus einem `backend`-Container liefert eine Adresse.

## Projektbezug

Modul 15 nutzt `MONGO_URL` erstmals tatsächlich im Backend-Code, um mit einem MongoDB-Treiber zu verbinden. Weiter geht es mit Lab 13.3: Ausblick auf Container in der CI-Pipeline.
