# Modul 12: Dockerfiles schreiben und optimieren

## Lab 12.1 - Dockerfile-Grundlagen

---

## Lab-Ziel

Du kannst für eine einfache Anwendung ein Dockerfile von Grund auf schreiben und die wichtigsten Anweisungen (`FROM`, `WORKDIR`, `COPY`, `RUN`, `CMD`, `ENV`) korrekt einsetzen.

**Leitfragen:**

<details>
<summary>Was ist der Unterschied zwischen `RUN` und `CMD`?</summary>

`RUN` wird beim Bauen des Images ausgeführt und hinterlässt eine neue Schicht; `CMD` legt nur den Standardbefehl fest, der beim Start eines Containers aus dem fertigen Image läuft.

</details>

<details>
<summary>Wozu dient `ENV` in einem Dockerfile?</summary>

Um Umgebungsvariablen für alle Container zu setzen, die aus diesem Image gestartet werden - z. B. Konfigurationswerte ohne Codeänderung.

</details>

<details>
<summary>Warum sollte jede Dockerfile-Anweisung möglichst wenig gleichzeitig verändern?</summary>

Jede Anweisung erzeugt eine eigene Schicht (Layer); kleine, klar abgegrenzte Schichten lassen sich beim erneuten Bauen gezielter cachen (Details in Lab 12.3).

</details>

---

## Dockerfile-Anweisungen im Überblick

| Anweisung | Zweck                                                                                |
| --------- | ------------------------------------------------------------------------------------ |
| `FROM`    | Basis-Image festlegen                                                                |
| `WORKDIR` | Arbeitsverzeichnis im Image setzen                                                   |
| `COPY`    | Dateien vom Build-Kontext ins Image kopieren                                         |
| `RUN`     | Befehl beim Bauen ausführen (z. B. Installation)                                     |
| `ENV`     | Umgebungsvariable für alle Container aus dem Image                                   |
| `EXPOSE`  | dokumentiert, welchen Port die Anwendung nutzt (rein informativ, öffnet keinen Port) |
| `CMD`     | Standardbefehl beim Containerstart                                                   |

---

## Beispiel: eine winzige Node-Anwendung

```js
// sample-app/greet.js
const name = process.env.GREET_NAME || "world";
console.log(`Hello, ${name}!`);
```

```dockerfile
# sample-app/Dockerfile
FROM node:24-alpine
WORKDIR /app
COPY greet.js .
ENV GREET_NAME=Docker
CMD ["node", "greet.js"]
```

```bash
docker build -t greet-sample sample-app/
docker run greet-sample
# Hello, Docker!
docker run -e GREET_NAME=Kurs greet-sample
# Hello, Kurs!
```

---

## Checkpoint

`docker run greet-sample` gibt `Hello, Docker!` aus; ein Überschreiben mit `-e GREET_NAME=...` ändert die Ausgabe entsprechend.

Weiter geht es mit Lab 12.2: das Backend-Image mit einem Multi-Stage-Build bauen und ausführen.
