# Modul 13: Mehrere Services mit Docker Compose verbinden

## Lab 13.1 - Mehrere Services verbinden

---

## Lab-Ziel

Du kannst mit einer `docker-compose.yml` zwei zusammengehörige Container (App + Datenbank) gemeinsam starten und ihre Erreichbarkeit über den Servicenamen verstehen.

**Leitfragen:**

<details>
<summary>Warum können sich zwei Compose-Services gegenseitig über ihren Servicenamen statt einer IP-Adresse erreichen?</summary>

Docker Compose legt für jedes Projekt ein eigenes, internes Netzwerk an, in dem der Servicename automatisch als DNS-Name auflösbar ist.

</details>

<details>
<summary>Was ist der Unterschied zwischen `docker run` mehrerer Container und `docker compose up`?</summary>

`docker compose up` liest alle Services aus einer Datei, erstellt automatisch ein gemeinsames Netzwerk und startet/stoppt sie als zusammengehörige Einheit statt einzeln mit separaten Befehlen.

</details>

---

## Minimalbeispiel: App + Redis

```yaml
# sample-compose/docker-compose.yml
services:
  cache:
    image: redis:7-alpine
  app:
    image: alpine
    command: sh -c "apk add --no-cache redis && redis-cli -h cache ping"
    depends_on:
      - cache
```

```bash
docker compose -f sample-compose/docker-compose.yml up
```

Erwartete Ausgabe von `app`: `PONG` - der `app`-Container erreicht `cache` über den Servicenamen `cache`, ganz ohne IP-Adresse.

- `depends_on` steuert nur die **Startreihenfolge**, nicht, ob der Zielservice bereits bereit zum Annehmen von Verbindungen ist.

---

## Checkpoint

`docker compose up` startet beide Services; der `app`-Container gibt `PONG` aus, was die Netzwerk-Erreichbarkeit über den Servicenamen bestätigt.

Weiter geht es mit Lab 13.2: `docker-compose.yml` für Backend und MongoDB.
