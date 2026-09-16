# Glossar: Fullstack Developer Toolbox

| Term / Abkürzung                                 | Plattform / Bereich            | Wann verwendet                                | Primäre Nutzer:innen | Vorkommen       |
| ------------------------------------------------ | ------------------------------ | --------------------------------------------- | -------------------- | --------------- |
| VS Code                                          | Editor                         | Gesamter Kurs                                 | Alle Teilnehmenden   | Modul 1         |
| GitHub Copilot                                   | KI-Assistenz                   | Codegenerierung, Commit-Nachrichten           | Alle Teilnehmenden   | Modul 1, 22     |
| Copilot Chat                                     | KI-Assistenz                   | Fragen zu Code, README-Generierung            | Alle Teilnehmenden   | Modul 1         |
| Extension                                        | VS Code                        | Editor-Konfiguration                          | Alle Teilnehmenden   | Modul 1         |
| Git                                              | Versionskontrolle              | Lokale Historie, Commits                      | Alle Teilnehmenden   | Modul 2         |
| Repository (Repo)                                | Git/GitHub                     | Projektcode versionieren                      | Alle Teilnehmenden   | Modul 2, 3      |
| Commit                                           | Git                            | Änderungen festhalten                         | Alle Teilnehmenden   | Modul 2         |
| `git log`                                        | Git-CLI                        | Historie einsehen                             | Alle Teilnehmenden   | Modul 2         |
| Branch                                           | Git                            | Parallele Entwicklung                         | Alle Teilnehmenden   | Modul 3         |
| Merge                                            | Git                            | Branches zusammenführen                       | Alle Teilnehmenden   | Modul 3         |
| Pull Request (PR)                                | GitHub                         | Code-Review vor Merge                         | Alle Teilnehmenden   | Modul 3         |
| GitHub Actions                                   | CI/CD                          | Automatisierte Pipelines                      | Alle Teilnehmenden   | Modul 4, 13     |
| CI/CD                                            | DevOps-Konzept                 | Automatisiertes Testen/Bauen                  | Alle Teilnehmenden   | Modul 4         |
| Workflow-Datei (`ci.yml`)                        | GitHub Actions                 | Pipeline-Definition                           | Alle Teilnehmenden   | Modul 4, 13     |
| YAML                                             | Konfigurationsformat           | Workflow-/Compose-Dateien                     | Alle Teilnehmenden   | Modul 4, 13     |
| Lint                                             | Codequalität                   | Statische Codeprüfung in CI                   | Alle Teilnehmenden   | Modul 4         |
| Build                                            | Node.js/TypeScript             | Kompilierung/CI-Schritt                       | Alle Teilnehmenden   | Modul 4, 6      |
| Node.js                                          | Laufzeitumgebung               | Backend-Ausführung                            | Alle Teilnehmenden   | Modul 5         |
| NPM                                              | Paketmanager                   | Abhängigkeiten installieren                   | Alle Teilnehmenden   | Modul 5         |
| Yarn                                             | Paketmanager                   | Alternative zu NPM                            | Alle Teilnehmenden   | Modul 5         |
| `package.json`                                   | Node.js                        | Projekt-Metadaten/Skripte                     | Alle Teilnehmenden   | Modul 5         |
| TypeScript                                       | Sprache                        | Typsicheres JavaScript                        | Alle Teilnehmenden   | Modul 6-9       |
| `tsconfig.json`                                  | TypeScript                     | Compiler-Konfiguration                        | Alle Teilnehmenden   | Modul 6         |
| Type Inference                                   | TypeScript                     | Automatische Typerkennung                     | Alle Teilnehmenden   | Modul 7         |
| Interface                                        | TypeScript                     | Datenmodell-Definition                        | Alle Teilnehmenden   | Modul 7         |
| `Ticket`-Interface                               | TeamBoard-Projekt              | Typisiertes Ticket-Datenmodell                | Alle Teilnehmenden   | Modul 7, 8      |
| `Status`-Typ                                     | TeamBoard-Projekt              | Zulässige Ticket-Status                       | Alle Teilnehmenden   | Modul 7         |
| Klasse                                           | TypeScript                     | Objektorientierte Struktur                    | Alle Teilnehmenden   | Modul 8         |
| Vererbung                                        | TypeScript/OOP                 | Klassenhierarchien                            | Alle Teilnehmenden   | Modul 8         |
| Access Modifier (`public`/`private`/`protected`) | TypeScript                     | Sichtbarkeit von Klassenfeldern               | Alle Teilnehmenden   | Modul 8         |
| Generics                                         | TypeScript                     | Wiederverwendbare typisierte Strukturen       | Alle Teilnehmenden   | Modul 8         |
| `Repository<T>`                                  | TeamBoard-Projekt              | Generische Datenhaltung                       | Alle Teilnehmenden   | Modul 8, 14     |
| `TicketRepository`                               | TeamBoard-Projekt              | Ticket-spezifische Datenhaltung               | Alle Teilnehmenden   | Modul 8, 14, 15 |
| `TicketService`                                  | TeamBoard-Projekt              | Ticket-Statuslogik                            | Alle Teilnehmenden   | Modul 8, 14     |
| WSL 2                                            | Windows-Subsystem              | Linux-Umgebung unter Windows                  | Windows-Nutzende     | Modul 10        |
| Container                                        | Docker/Virtualisierung         | Isolierte Laufzeitumgebung                    | Alle Teilnehmenden   | Modul 10-13     |
| Virtuelle Maschine (VM)                          | Virtualisierung                | Vergleich zu Containern                       | Alle Teilnehmenden   | Modul 10        |
| Docker                                           | Container-Plattform            | Anwendungen containerisieren                  | Alle Teilnehmenden   | Modul 10-13     |
| Docker CLI                                       | Docker                         | Container/Images verwalten                    | Alle Teilnehmenden   | Modul 11        |
| Image                                            | Docker                         | Vorlage für Container                         | Alle Teilnehmenden   | Modul 11, 12    |
| Dockerfile                                       | Docker                         | Bauanleitung für Images                       | Alle Teilnehmenden   | Modul 11, 12    |
| `docker build`                                   | Docker-CLI                     | Image aus Dockerfile erzeugen                 | Alle Teilnehmenden   | Modul 11, 12    |
| `docker run`                                     | Docker-CLI                     | Container starten                             | Alle Teilnehmenden   | Modul 11        |
| Layer-Caching                                    | Docker                         | Schnellere wiederholte Builds                 | Alle Teilnehmenden   | Modul 12        |
| Multi-Stage Build                                | Docker                         | Kleinere, optimierte Images                   | Alle Teilnehmenden   | Modul 12        |
| Docker Compose                                   | Docker                         | Mehrere Services gemeinsam starten            | Alle Teilnehmenden   | Modul 13-19     |
| `docker-compose.yml`                             | Docker Compose                 | Service-Definitionen                          | Alle Teilnehmenden   | Modul 13-19     |
| Volume                                           | Docker                         | Persistente Datenspeicherung                  | Alle Teilnehmenden   | Modul 13        |
| `depends_on`                                     | Docker Compose                 | Startreihenfolge von Services                 | Alle Teilnehmenden   | Modul 13        |
| `docker compose config`                          | Docker Compose                 | Konfiguration validieren                      | Alle Teilnehmenden   | Modul 13        |
| REST                                             | API-Architekturstil            | Ressourcenbasierte HTTP-API                   | Alle Teilnehmenden   | Modul 14        |
| HTTP-Methode (`GET`/`POST`/`PATCH`)              | HTTP                           | Aktion auf eine Ressource                     | Alle Teilnehmenden   | Modul 14        |
| Statuscode (`200`/`201`/`400`/`404`)             | HTTP                           | Ergebnis einer Anfrage                        | Alle Teilnehmenden   | Modul 14        |
| Express                                          | Node.js-Framework              | HTTP-Server/Routen                            | Alle Teilnehmenden   | Modul 14-16, 19 |
| Middleware                                       | Express                        | Anfrage-Vorverarbeitung                       | Alle Teilnehmenden   | Modul 16, 19    |
| Route                                            | Express                        | Endpunkt-Definition                           | Alle Teilnehmenden   | Modul 14        |
| `app.listen`                                     | Express                        | Server dauerhaft starten                      | Alle Teilnehmenden   | Modul 14        |
| GraphQL                                          | API-Architekturstil            | Flexible, feldbasierte Abfragen               | Alle Teilnehmenden   | Modul 15        |
| Query (GraphQL)                                  | GraphQL                        | Daten lesen                                   | Alle Teilnehmenden   | Modul 15        |
| Mutation (GraphQL)                               | GraphQL                        | Daten verändern                               | Alle Teilnehmenden   | Modul 15        |
| Resolver                                         | GraphQL                        | Implementierung von Query/Mutation            | Alle Teilnehmenden   | Modul 15        |
| Schema / `typeDefs`                              | GraphQL                        | Typdefinitionen der API                       | Alle Teilnehmenden   | Modul 15        |
| Apollo Server                                    | GraphQL-Bibliothek             | GraphQL-Server in Node.js                     | Alle Teilnehmenden   | Modul 15        |
| SQL                                              | Relationale Datenbanken        | Tabellenbasierte Datenhaltung                 | Alle Teilnehmenden   | Modul 15        |
| NoSQL                                            | Dokumentenbasierte Datenbanken | Flexible Datenhaltung                         | Alle Teilnehmenden   | Modul 15        |
| MongoDB                                          | NoSQL-Datenbank                | Ticket-Persistenz                             | Alle Teilnehmenden   | Modul 13, 15    |
| Collection                                       | MongoDB                        | Gruppe von Dokumenten                         | Alle Teilnehmenden   | Modul 15        |
| Dokument (MongoDB)                               | MongoDB                        | Einzelner Datensatz                           | Alle Teilnehmenden   | Modul 15        |
| `MongoClient`                                    | MongoDB-Treiber                | Verbindungsaufbau                             | Alle Teilnehmenden   | Modul 15        |
| `MONGO_URL`                                      | Umgebungsvariable              | MongoDB-Verbindungsstring                     | Alle Teilnehmenden   | Modul 13, 15    |
| JWT (JSON Web Token)                             | Authentifizierung              | Zustandsloser Login-Nachweis                  | Alle Teilnehmenden   | Modul 16        |
| OAuth                                            | Authentifizierung              | Delegierter Login über Drittanbieter          | Alle Teilnehmenden   | Modul 16        |
| `bcrypt`                                         | Node.js-Bibliothek             | Passwort-Hashing                              | Alle Teilnehmenden   | Modul 16        |
| Hashing                                          | Sicherheitskonzept             | Passwörter irreversibel speichern             | Alle Teilnehmenden   | Modul 16        |
| `Authorization`-Header                           | HTTP                           | Token bei Anfragen mitsenden                  | Alle Teilnehmenden   | Modul 16, 19    |
| Bearer-Token                                     | Authentifizierung              | Trägerbasierte Autorisierung                  | Alle Teilnehmenden   | Modul 16        |
| `requireAuth`                                    | TeamBoard-Projekt              | Express-Middleware für Auth                   | Alle Teilnehmenden   | Modul 16        |
| `JWT_SECRET`                                     | Umgebungsvariable              | Signaturschlüssel für Tokens                  | Alle Teilnehmenden   | Modul 16        |
| CORS                                             | Web-Sicherheit                 | Cross-Origin-Anfragen erlauben                | Alle Teilnehmenden   | Modul 19        |
| Emmet                                            | Editor-Werkzeug                | Schnelles HTML-Schreiben                      | Alle Teilnehmenden   | Modul 17        |
| CSS Grid                                         | CSS                            | Zweidimensionales Layout                      | Alle Teilnehmenden   | Modul 17        |
| Flexbox                                          | CSS                            | Eindimensionales Layout                       | Alle Teilnehmenden   | Modul 17        |
| Media Query                                      | CSS                            | Bedingtes Styling nach Breite                 | Alle Teilnehmenden   | Modul 17        |
| Breakpoint                                       | Responsive Design              | Umbruchpunkt zwischen Layouts                 | Alle Teilnehmenden   | Modul 17        |
| Bootstrap 5                                      | CSS-Framework                  | Fertige responsive Klassen                    | Alle Teilnehmenden   | Modul 17-19     |
| Sass / SCSS                                      | CSS-Präprozessor               | Variablen, Verschachtelung                    | Alle Teilnehmenden   | Modul 17, 18    |
| Sass-Variable                                    | Sass                           | Wiederverwendbare Werte                       | Alle Teilnehmenden   | Modul 17        |
| Verschachtelung (`&`)                            | Sass                           | Selektoren ineinander schreiben               | Alle Teilnehmenden   | Modul 17        |
| Gulp                                             | Build-Werkzeug                 | Sass-zu-CSS-Automatisierung                   | Alle Teilnehmenden   | Modul 17        |
| `gulpfile.js`                                    | Gulp                           | Task-Definition                               | Alle Teilnehmenden   | Modul 17        |
| Watch-Modus                                      | Gulp                           | Automatisches Neu-Kompilieren                 | Alle Teilnehmenden   | Modul 17        |
| React                                            | Frontend-Bibliothek            | Komponentenbasierte SPA                       | Alle Teilnehmenden   | Modul 18, 19    |
| Komponente (React)                               | React                          | Wiederverwendbarer UI-Baustein                | Alle Teilnehmenden   | Modul 18        |
| Props                                            | React                          | Von außen übergebene Daten                    | Alle Teilnehmenden   | Modul 18        |
| State                                            | React                          | Interner, veränderlicher Zustand              | Alle Teilnehmenden   | Modul 18        |
| `useState`                                       | React-Hook                     | Lokalen Zustand verwalten                     | Alle Teilnehmenden   | Modul 18        |
| `useEffect`                                      | React-Hook                     | Nebenwirkungen (z. B. Datenladen)             | Alle Teilnehmenden   | Modul 19        |
| JSX                                              | React                          | HTML-ähnliche Syntax in TypeScript            | Alle Teilnehmenden   | Modul 18        |
| SPA (Single Page Application)                    | Frontend-Architektur           | Seite ohne vollständiges Neuladen             | Alle Teilnehmenden   | Modul 18        |
| Vite                                             | Build-Werkzeug                 | React-Projekt-Setup                           | Alle Teilnehmenden   | Modul 18        |
| `TicketCard`                                     | TeamBoard-Projekt              | Ticket-Darstellungskomponente                 | Alle Teilnehmenden   | Modul 18, 19    |
| `Column`                                         | TeamBoard-Projekt              | Spalten-Komponente je Status                  | Alle Teilnehmenden   | Modul 18, 19    |
| `LoginForm`                                      | TeamBoard-Projekt              | Login-Formular-Komponente                     | Alle Teilnehmenden   | Modul 19        |
| `NewTicketForm`                                  | TeamBoard-Projekt              | Ticket-Anlage-Komponente                      | Alle Teilnehmenden   | Modul 19        |
| Angular                                          | Frontend-Framework             | Vergleichsalternative zu React                | Alle Teilnehmenden   | Modul 20        |
| `@Component`                                     | Angular                        | Dekorator für Komponenten                     | Alle Teilnehmenden   | Modul 20        |
| `@Input()`                                       | Angular                        | Props-Äquivalent                              | Alle Teilnehmenden   | Modul 20        |
| `NgModule`                                       | Angular                        | Gruppierung von Komponenten                   | Alle Teilnehmenden   | Modul 20        |
| Zweiseitige Datenbindung                         | Angular                        | `[(ngModel)]`-Konzept                         | Alle Teilnehmenden   | Modul 20        |
| Azure                                            | Cloud-Plattform                | Deployment-Zielumgebung                       | Alle Teilnehmenden   | Modul 21        |
| Azure Static Web Apps                            | Azure-Dienst                   | Hosting statischer Frontend-Builds            | Alle Teilnehmenden   | Modul 21        |
| `dist/`-Ordner                                   | Vite-Build                     | Statisches Produktionsergebnis                | Alle Teilnehmenden   | Modul 21        |
| Kanban                                           | Projektmanagement-Methode      | Ticket-Statusfluss (To Do/In Progress/Done)   | Alle Teilnehmenden   | Gesamter Kurs   |
| TeamBoard                                        | Durchgehendes Kursprojekt      | Ticket-System als Kursziel                    | Alle Teilnehmenden   | Gesamter Kurs   |
| Ticket                                           | TeamBoard-Datenmodell          | Titel, Beschreibung, Zuweisung, Status        | Alle Teilnehmenden   | Ab Modul 7      |
| Assignee                                         | TeamBoard-Datenmodell          | Zugewiesene Person eines Tickets              | Alle Teilnehmenden   | Ab Modul 7      |
| Umgebungsvariable                                | Konfiguration                  | Geheimnisse/Konfiguration außerhalb des Codes | Alle Teilnehmenden   | Modul 13, 16    |
| Checkpoint                                       | Didaktisches Element           | Überprüfbares Zwischenziel je Lab             | Alle Teilnehmenden   | Gesamter Kurs   |
| Kapstone (Capstone)                              | Didaktisches Element           | Abschließende Gesamtdemo                      | Alle Teilnehmenden   | Modul 22        |
| Trainer-Demo                                     | Didaktisches Element           | Vorführung ohne Teilnehmerübung               | Alle Teilnehmenden   | Modul 20, 21    |
| Puffer (Kurszeit)                                | Zeitplanung                    | Reserve für offene Fragen                     | Alle Teilnehmenden   | Modul 9         |
| Fallback                                         | Didaktisches Element           | Alternative bei technischen Problemen         | Alle Teilnehmenden   | Gesamter Kurs   |
