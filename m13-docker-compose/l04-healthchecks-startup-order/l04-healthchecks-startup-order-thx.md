# Modul 13: Docker Compose

## Lab 13.4 - Vertiefung: Healthchecks und Startreihenfolge

> Wird **nach Lab 14.3** bearbeitet - erst dann läuft das Backend dauerhaft im Container.

---

## Lab-Ziel

`depends_on` aus Lab 13.1 wartet nur, bis ein Container **gestartet** ist, nicht bis der Dienst darin **bereit** ist. Du ergänzt einen Healthcheck, damit das Backend erst startet, wenn MongoDB tatsächlich Verbindungen annimmt.

**Leitfragen:**

<details>
<summary>Warum reicht "Container läuft" als Signal nicht?</summary>

Ein Datenbank-Container ist nach wenigen Millisekunden "gestartet", braucht aber einige Sekunden, bis er Verbindungen annimmt. Startet das Backend in dieser Lücke und verbindet sich sofort, schlägt der erste Verbindungsversuch fehl. Ab Modul 15 verbindet sich das Backend beim Start mit MongoDB - dann wird aus der Lücke ein echter Fehler.

</details>

<details>
<summary>Was ist ein Healthcheck aus Sicht von Docker?</summary>

Ein Befehl, den Docker in regelmäßigen Abständen **im Container** ausführt. Exit-Code 0 heißt gesund, alles andere ungesund. Docker führt den Zustand als `starting`, `healthy` oder `unhealthy`.

</details>

---

## Die Bausteine

```yaml
mongo:
  image: mongo:8
  healthcheck:
    test: [...]          # Befehl im Container, Exit-Code 0 = gesund
    interval: 5s         # wie oft geprüft wird
    timeout: 3s          # wie lange ein einzelner Test dauern darf
    retries: 10          # so viele Fehlschläge in Folge, dann "unhealthy"
    start_period: 10s    # Anlaufzeit: Fehlschläge zählen hier noch nicht
```

```yaml
backend:
  depends_on:
    mongo:
      condition: service_healthy   # statt der kurzen Listenform "- mongo"
```

Das offizielle `mongo`-Image bringt die Shell `mongosh` mit. Mit `mongosh --eval` lässt sich ein einzelner Befehl ausführen - der Rest ist eure Aufgabe.

---

## Brücke zu dem, was du kennst

Dasselbe Prinzip steckt hinter Kubernetes' `readinessProbe` und hinter Spring Boots `/actuator/health`: Nicht "Prozess läuft", sondern "Dienst kann arbeiten" ist das Signal, auf das andere warten.

---

## Checkpoint

`docker compose up -d` zeigt beim Start `Waiting` und `Healthy` für `mongo`, **bevor** `backend` startet. `docker compose ps` zeigt `mongo` mit dem Zusatz `(healthy)`.

## Projektbezug

Ab Modul 15 verbindet sich das Backend beim Start mit MongoDB. Mit dem Healthcheck braucht der Fallback "einfach nochmal `up` ausführen" aus Lab 15.3 nicht mehr.
