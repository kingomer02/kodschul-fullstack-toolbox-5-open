# Modul 22: Projekt-Abschluss und Rückblick

## Lab 22.1 - Projekt-Rückblick

---

## Lab-Ziel

Du kannst die vollständige Kette aller in diesem Kurs gebauten TeamBoard-Bausteine in der richtigen Reihenfolge benennen und ihr Zusammenspiel in einer Live-Demo zeigen.

**Leitfragen:**

<details>
<summary>Welche vier Hauptstationen hat TeamBoard von Modul 1 bis Modul 19 durchlaufen?</summary>

Grundlagen/Git/GitHub mit CI (Module 1-9) → Containerisierung mit Docker/Compose (Module 10-13) → REST/GraphQL-API über MongoDB mit JWT-Absicherung (Module 14-16) → responsive React-Oberfläche (Module 17-19).

</details>

<details>
<summary>Warum war die Reihenfolge (erst Backend/Daten, dann Absicherung, dann Oberfläche) sinnvoll?</summary>

Die Oberfläche in Modul 19 konnte erst gegen eine echte, abgesicherte API entwickelt werden, nachdem diese API (Modul 14-16) bereits existierte - andernfalls hätte das Frontend gegen eine sich noch ändernde Grundlage entwickelt werden müssen.

</details>

---

## Die komplette Kette im Überblick

| Bereich                | Module | Ergebnis                                                                |
| ---------------------- | ------ | ----------------------------------------------------------------------- |
| Werkzeuge & Grundlagen | 1-9    | VS Code/Copilot, Git/GitHub, CI-Pipeline, Node/TypeScript-Grundlagen    |
| Containerisierung      | 10-13  | Backend im Container, `docker-compose.yml` mit MongoDB                  |
| API & Daten            | 14-16  | REST + GraphQL über MongoDB, JWT-Login, geschützte Routen               |
| Oberfläche             | 17-19  | Responsive Kanban-Board mit Bootstrap/Sass/React, verbunden mit der API |
| Ausblick               | 20-21  | Angular als Vergleich, Azure als Cloud-Deployment-Konzept               |

---

## Live-Demo-Ablauf

1. `docker compose up -d --build` im Projekt-Root sowie `npm run dev` im `frontend/`-Ordner starten.
2. Im Browser einloggen, ein neues Ticket anlegen und es zweimal über "Weiter →" bis "Done" bewegen.
3. Parallel `docker compose logs backend` zeigen, um die REST-Aufrufe im Hintergrund sichtbar zu machen.
4. Kurz auf `git log --oneline` verweisen, um zu zeigen, wie viele einzelne, nachvollziehbare Commits zu diesem Endergebnis geführt haben.

---

## Checkpoint

Ein Ticket wird live vor der Gruppe angelegt, zugewiesen und bis "Done" bewegt - alle Beteiligten sehen dieselbe Änderung sowohl in der Oberfläche als auch in den Backend-Logs.

Weiter geht es mit Lab 22.2: Rückblick auf die Copilot-Workflows aus Modul 1-2.
