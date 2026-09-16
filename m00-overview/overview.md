# Kursüberblick: Fullstack Developer Toolbox

## Kursziel und sichtbares Endergebnis

Am Ende des Kurses steht **TeamBoard**, ein containerisiertes Kanban-Ticketsystem, das die Teilnehmenden Modul für Modul selbst gebaut haben:

- versioniert mit Git/GitHub, abgesichert durch eine grüne CI-Pipeline (GitHub Actions),
- containerisiert mit Docker und Docker Compose (Backend + MongoDB),
- mit REST- **und** GraphQL-API über MongoDB, Routen durch JWT abgesichert,
- bedient über eine responsive React-Oberfläche mit Login, Ticket-Erstellung und Statuswechsel.

Sichtbarer Abschluss: eine Live-Demo in Modul 22, in der ein Ticket vor der Gruppe angelegt, zugewiesen und von "To Do" über "In Progress" bis "Done" bewegt wird.

## Zielgruppe und bestätigte Voraussetzungen

- **Rolle:** professionelle Webentwickler:innen, die ihr Werkzeug-Wissen vertiefen.
- **Vorkenntnisse:** HTML/CSS/JavaScript-Grundlagen, praktische Web-Entwicklungserfahrung, OOP-Konzepte (Einstufung: Intermediate).
- **Gruppengröße:** maximal 2 Teilnehmende - individuelles Tempo möglich, kein Grund-/Vertiefungs-Split nötig.
- **Lokale Installationen vor Kursbeginn:** VS Code, Node.js, Git, Docker Desktop, WSL 2 (Windows).

## Vollständige Agenda

### Tag 1 - Setup, Git & GitHub

| Zeit        | Modul                             | Inhalt                                  |
| ----------- | --------------------------------- | --------------------------------------- |
| 09:00-09:20 | -                                 | Vorstellung, Installationscheck         |
| 09:20-10:30 | Modul 1: VS Code & Copilot        | Editor-Konfiguration, Copilot-Workflows |
| 10:45-12:15 | Modul 2: Git-Grundlagen           | Repo anlegen, Commits, Historie         |
| 13:15-14:45 | Modul 3: GitHub                   | Push, Branching, Pull Requests          |
| 15:00-16:30 | Modul 4: CI/CD mit GitHub Actions | Workflow-Datei, Lint/Build-Pipeline     |

**Checkpoint:** Grüner CI-Lauf auf GitHub sichtbar.

### Tag 2 - Node.js & TypeScript

| Zeit        | Modul                          | Inhalt                               |
| ----------- | ------------------------------ | ------------------------------------ |
| 09:00-09:45 | Modul 5: Node.js               | Grundlagen, NPM/Yarn                 |
| 09:45-10:30 | Modul 6: TypeScript-Einstieg   | Vorteile, tsconfig-Setup             |
| 10:45-12:15 | Modul 7: TypeScript-Grundlagen | Basistypen, Interfaces, Datenmodelle |
| 13:15-14:45 | Modul 8: TypeScript-OOP        | Klassen, Access Modifiers, Generics  |
| 15:00-16:30 | Modul 9: JS/TS-Puffer          | Offene Fragen, vertiefende Übung     |

**Checkpoint:** `TicketService`/`TicketRepository`-Klassen instanziierbar.

### Tag 3 - Docker & WSL 2

| Zeit        | Modul                        | Inhalt                                              |
| ----------- | ---------------------------- | --------------------------------------------------- |
| 09:00-10:30 | Modul 10: Container-Einstieg | WSL 2, Container vs. VM, Ökosystem                  |
| 10:45-12:15 | Modul 11: Docker-Grundlagen  | CLI, Images vs. Container, Backend containerisieren |
| 13:15-14:45 | Modul 12: Docker-Images      | Dockerfile-Optimierung, Layer-Caching               |
| 15:00-16:30 | Modul 13: Docker Compose     | Mehrere Services verbinden, CI-Ausblick             |

**Checkpoint:** Backend und MongoDB gemeinsam per Compose erreichbar.

### Tag 4 - APIs, Datenbanken & responsive UI

| Zeit        | Modul                       | Inhalt                                                |
| ----------- | --------------------------- | ----------------------------------------------------- |
| 09:00-10:30 | Modul 14: REST-API          | Ressourcen, Statuscodes, Express-API im Container     |
| 10:45-12:15 | Modul 15: GraphQL & MongoDB | Queries/Mutations, SQL vs. NoSQL, MongoDB-Integration |
| 13:15-14:45 | Modul 16: Authentifizierung | JWT/OAuth-Grundlagen, Login-Flow, geschützte Routen   |
| 15:00-16:30 | Modul 17: Frontend-Styling  | Emmet, Grid/Flexbox, Bootstrap 5, Sass, Gulp          |

**Checkpoint:** Geschützte API lehnt unauthentifizierte Anfragen ab, akzeptiert authentifizierte.

### Tag 5 - Single Page Applications & Cloud-Deployment

| Zeit        | Modul                             | Inhalt                                         |
| ----------- | --------------------------------- | ---------------------------------------------- |
| 09:00-10:30 | Modul 18: React-Einstieg          | SPA-Konzepte, Komponenten/State, Projekt-Setup |
| 10:45-12:15 | Modul 19: React-API-Integration   | Login, Datenfluss, Aktionen aus der Oberfläche |
| 13:15-13:45 | Modul 20: Angular (Demo)          | Grundkonzepte, Vergleich zu React              |
| 13:45-14:15 | Modul 21: Azure-Deployment (Demo) | Deployment-Grundlagen, Static Web Apps         |
| 15:00-16:30 | Modul 22: Abschluss               | Projekt-Rückblick, Copilot-Rückblick, Q&A      |

**Checkpoint:** Vollständige Kette live demonstriert (Login → Ticket anlegen → Status ändern → Done).

## Modul- und Projektstruktur

- 22 durchnummerierte Module, jedes mit 2-5 Labs (`l01`, `l02`, ...).
- Jedes Lab folgt dem Muster **Theorie (`-thx.md`) → generische Übung (`-exc.md`/`-sol.md`) → TeamBoard-Transferübung** (`mXX-exc.md`/`mXX-sol.md` je Modul).
- Ausnahme: Modul 9 (reiner Puffer), Modul 20/21 (reine Trainer-Demo ohne Teilnehmerübung), Modul 22 (Kapstone-Rückblick statt neuer Projektschritt).
- TeamBoard läuft als durchgehendes Projekt über alle 22 Module - jede Änderung baut auf der vorherigen auf.

## Arbeitsweise und Übungs-Konventionen

- Jedes Thema startet mit einem **generischen Beispiel** (losgelöst von TeamBoard), gefolgt von der **Aufbau-Übung** am eigenen Projekt.
- Checkpoints am Ende jedes Labs/Moduls machen den erreichten Stand konkret überprüfbar (z. B. "`docker ps` zeigt den Container").
- Fallback-Hinweise in jeder Übung decken die häufigsten technischen Stolpersteine ab (z. B. Netzwerkprobleme, Versionskonflikte).

## Umgebung und Sicherheits-Grundlagen

- Lokale Installationen (VS Code, Node.js, Git, Docker Desktop, WSL 2) werden vor Tag 1 geprüft.
- Ab Modul 10 läuft die Entwicklung containerisiert - ein funktionierendes Docker-Desktop-Setup ist ab diesem Punkt Voraussetzung für alle Folgemodule.
- Geheimnisse (z. B. `JWT_SECRET`) liegen ausschließlich in Umgebungsvariablen, nie im Code (Modul 16).
- Passwörter werden ausschließlich gehasht gespeichert, nie im Klartext (Modul 16).

## Teilnehmer-Vorstellung

Zu Beginn von Tag 1 stellt sich jede Person kurz vor:

- Name und Rolle,
- fachlicher Hintergrund und Weg in die Webentwicklung,
- Organisation und Betriebszugehörigkeit,
- optional: Stadt/Region und aktuelles Wetter,
- bisherige Erfahrung mit den Kursthemen (Docker, REST/GraphQL, React, Angular),
- Erwartungen an den Kurs,
- ein konkretes Einsatzszenario, für das die Kursinhalte genutzt werden sollen.

Persönliche Angaben (z. B. Stadt/Wetter) können übersprungen werden, wenn gewünscht.
