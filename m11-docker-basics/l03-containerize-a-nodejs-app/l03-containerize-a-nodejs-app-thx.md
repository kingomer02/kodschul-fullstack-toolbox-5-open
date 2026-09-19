# Modul 11: Docker-Grundlagen

## Lab 11.3 - Eine Node.js-App containerisieren

---

## Lab-Ziel

Du kannst für eine bestehende Node.js/TypeScript-Anwendung ein einfaches, lauffähiges Dockerfile schreiben und daraus einen Container starten.

**Leitfragen:**

<details>
<summary>Warum wird zuerst nur `package.json` kopiert und `npm ci` ausgeführt, bevor der restliche Code kopiert wird?</summary>

Damit Docker die Abhängigkeits-Schicht separat cachen kann - ändert sich nur der Quellcode, nicht aber `package.json`, muss `npm ci` beim nächsten Build nicht erneut laufen.

</details>

<details>
<summary>Warum `npm ci` statt `npm install` im Dockerfile?</summary>

`npm ci` installiert exakt die in `package-lock.json` festgelegten Versionen und ist für reproduzierbare, automatisierte Builds gedacht; `npm install` kann den Lock-File unter Umständen verändern.

</details>

<details>
<summary>Was passiert mit `CMD`, wenn der Container gestartet wird?</summary>

`CMD` legt den Standardbefehl fest, der beim Start des Containers ausgeführt wird - hier der kompilierte TypeScript-Code (`node dist/index.js`).

</details>

---

## Ein einfaches Dockerfile für das Backend

```dockerfile
# backend/Dockerfile
FROM node:24-alpine

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci

COPY . .
RUN npm run build

CMD ["node", "dist/index.js"]
```

- `FROM node:24-alpine`: schlankes Basis-Image, wie in Modul 10 geplant.
- `WORKDIR /app`: alle folgenden Befehle laufen relativ zu `/app` im Container.
- Die Reihenfolge (erst `package.json`, dann `npm ci`, dann restlicher Code) nutzt Docker-Layer-Caching - Details dazu folgen in Modul 12.

---

## `.dockerignore`

```text
node_modules
dist
.git
```

Verhindert, dass lokale `node_modules`/`dist`-Ordner unnötig in den Build-Kontext kopiert werden.

---

## Bauen und Ausführen

```bash
docker build -t teamboard-backend .
docker run --name teamboard-backend teamboard-backend
docker logs teamboard-backend
```

Erwartete Ausgabe: dieselbe Konsolenausgabe wie beim lokalen `npm start` aus der Modul-8-Transfer-Übung (Status-Übergänge `To Do -> In Progress -> Done`).

---

## Checkpoint

`docker ps -a` zeigt den Container `teamboard-backend`; `docker logs teamboard-backend` zeigt die erwarteten Status-Übergänge.

## Projektbezug

Ab hier existiert ein erstes, funktionierendes Dockerfile für das Backend. Modul 12 optimiert Layer-Caching und Image-Größe; Modul 13 verbindet das Backend containerisiert mit MongoDB.
