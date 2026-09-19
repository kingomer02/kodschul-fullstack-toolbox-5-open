# Best Practices: Fullstack Developer Toolbox

Diese Liste bündelt modulübergreifende Praktiken, die im Kurs konsequent angewendet werden. Jeder Punkt nennt den Grund oder das Entscheidungskriterium, nicht nur die Regel selbst.

## Versionskontrolle und Zusammenarbeit (Modul 1-4)

**Kleine, aussagekräftige Commits statt Sammel-Commits.**
Jede Änderung lässt sich einzeln nachvollziehen und im Zweifel gezielt rückgängig machen - ein einziger riesiger Commit am Ende eines Moduls würde diese Nachvollziehbarkeit zerstören.

**Feature-Branches statt direkter Commits auf `main`.**
`main` bleibt jederzeit in einem funktionierenden Zustand; ein Fehler in einem Branch betrifft nur diesen Branch, nicht die gemeinsame Basis.

**Pull Requests auch bei einer Gruppengröße von zwei Personen.**
Der PR-Workflow selbst ist die zu übende Fähigkeit - unabhängig von der Gruppengröße entspricht er dem in der Praxis üblichen Ablauf.

**CI-Pipeline so früh wie möglich einrichten (Modul 4), nicht erst am Kursende.**
Ein grüner CI-Lauf gibt ab diesem Zeitpunkt bei jedem weiteren Modul sofortiges Feedback, ob eine Änderung die Grundstruktur des Projekts bricht.

## TypeScript und Datenmodellierung (Modul 6-8)

**Datenmodelle als `interface` definieren, bevor Logik darauf aufbaut.**
Ein typisiertes `Ticket`-Interface (Modul 7) verhindert, dass später fehlerhafte Felder (z. B. ein falsch geschriebenes `status`-Feld) unbemerkt durchrutschen.

**Zustand und Logik in separaten Klassen halten (`TicketRepository` vs. `TicketService`).**
Datenhaltung (Repository) und fachliche Regeln (Service, z. B. Statuswechsel) bleiben unabhängig austauschbar - ein Wechsel von In-Memory zu MongoDB (Modul 15) betrifft dadurch **hauptsächlich** das Repository.

> **Korrektur (Durchlauf 09/2026, Ö. Akgeyik):** Im Original stand hier „betrifft dadurch nur das Repository, nicht den Service“. Das stimmt so nicht: Der Zugriff auf MongoDB ist asynchron, und `async`/`await` zieht sich durch alle aufrufenden Schichten - der Service muss also mitgeändert werden. Die Trennung spart trotzdem Arbeit, aber sie ist keine Garantie dafür, dass eine Schicht unberührt bleibt.

**Generics (`Repository<T>`) nutzen, statt Datenhaltungscode für jede Ressource zu duplizieren.**
Eine einzige, getestete Implementierung deckt sowohl Tickets als auch zukünftige Ressourcen ab, ohne Code zu wiederholen.

## Containerisierung (Modul 10-13)

**Multi-Stage-Builds für Produktions-Images verwenden (Modul 12).**
Build-Werkzeuge (z. B. der TypeScript-Compiler) landen nicht im finalen Image - das Ergebnis ist kleiner und hat eine geringere Angriffsfläche.

**`npm ci` statt `npm install` im Dockerfile verwenden.**
`npm ci` installiert exakt die in `package-lock.json` festgehaltenen Versionen und bricht bei Inkonsistenzen ab - reproduzierbare Builds sind in einem containerisierten Projekt besonders wichtig.

**Docker-Compose-Konfiguration in CI validieren (`docker compose config`, Modul 13), statt sie ungeprüft zu lassen.**
Ein Syntaxfehler in `docker-compose.yml` wird so schon beim nächsten Push sichtbar, statt erst beim nächsten manuellen `docker compose up` bemerkt zu werden.

**Benannte Volumes für Datenbank-Container verwenden (Modul 13).**
Ohne ein Volume gingen alle MongoDB-Daten bei jedem Container-Neustart verloren - ein benanntes Volume übersteht das.

## APIs und Datenhaltung (Modul 14-16)

**Konsistente HTTP-Statuscodes verwenden (`200`/`201`/`400`/`404`), statt bei jedem Endpunkt neu zu entscheiden.**
Aufrufende Systeme (auch das eigene Frontend) können sich auf ein einheitliches Verhalten verlassen, statt für jeden Endpunkt eine eigene Fehlerbehandlung zu bauen.

**Datenzugriff hinter dem Repository kapseln, auch wenn REST und GraphQL parallel existieren (Modul 15).**
Beide APIs rufen dieselben Repository-Methoden auf - eine Änderung an der Datenhaltung muss nur an einer Stelle erfolgen.

**Passwörter ausschließlich gehasht speichern (`bcrypt`, Modul 16), nie im Klartext.**
Bei einem Datenbank-Leck bleiben gehashte Passwörter praktisch nutzlos für Angreifende, Klartext-Passwörter wären sofort kompromittiert.

**Geheimnisse (`JWT_SECRET`, `MONGO_URL`) als Umgebungsvariablen halten, nie im Code.**
Ein im Code hinterlegtes Geheimnis wird mit jedem Blick in den Quellcode (z. B. auf GitHub) offengelegt - eine Umgebungsvariable bleibt getrennt vom versionierten Code.

**Middleware zentral registrieren (`app.use("/tickets", requireAuth)`), statt sie bei jeder Route zu wiederholen.**
Eine einzige Stelle für die Zugriffsprüfung ist leichter zu warten und zu überprüfen als über viele Routen verstreute Einzelprüfungen.

## Frontend-Styling (Modul 17)

**Fertige Frameworks (Bootstrap) für Grundlayout nutzen, eigenes CSS nur für spezifische Anpassungen (Sass).**
Bootstrap deckt getestete, responsive Grundmuster ab - eigene Sass-Variablen ergänzen nur das, was projektspezifisch ist (z. B. Statusfarben), ohne das Rad neu zu erfinden.

**Build-Schritte automatisieren (Gulp), statt manuell zu kompilieren.**
Ein Watch-Task erkennt Änderungen sofort und kompiliert automatisch neu - ohne ihn müsste nach jeder Sass-Änderung ein Befehl von Hand ausgeführt werden, was leicht vergessen wird.

## React und API-Anbindung (Modul 18-19)

**Datenladen in `useEffect` kapseln, nie direkt im Komponentenkörper.**
Ohne `useEffect` würde bei jedem Rendern ein neuer Netzwerkaufruf ausgelöst - mit `useEffect` und passendem Abhängigkeitsarray passiert das kontrolliert, z. B. nur einmal oder bei Token-Änderung.

**Nach jeder schreibenden Aktion (Ticket anlegen, Status ändern) die Daten neu laden, statt den lokalen State manuell zu verändern.**
Ein erneuter Abruf garantiert, dass die Oberfläche exakt den tatsächlichen Datenbankstand zeigt, statt auf riskante Annahmen über den neuen Zustand zu setzen.

**Props für von außen kommende Daten, State nur für tatsächlich innerhalb der Komponente veränderliche Werte verwenden.**
Eine klare Trennung verhindert Verwirrung darüber, wer für eine Änderung "zuständig" ist - die aufrufende Komponente (Props) oder die Komponente selbst (State).

**Eindeutige `key`-Werte bei Listen verwenden (z. B. Ticket-`id`).**
Ohne eindeutige Keys kann React Listenänderungen nicht zuverlässig nachvollziehen und rendert im schlimmsten Fall falsche oder doppelte Elemente.

## Sicherheit (übergreifend)

**CORS bewusst und möglichst eng konfigurieren.**
Ein in diesem Kurs bewusst offen gehaltenes `cors()` (Modul 19) ist für die Lernumgebung ausreichend, sollte in einer echten Produktionsumgebung aber auf konkrete erlaubte Ursprünge eingeschränkt werden.

**Fehlerfälle (falscher Login, fehlender Token, unbekannte Ticket-ID) explizit testen, nicht nur den Erfolgsfall.**
Nur wer den Fehlerfall bewusst prüft (z. B. `401` bei fehlendem Token), kann sicher sein, dass eine Absicherung tatsächlich wirkt und nicht nur zufällig funktioniert.

## Allgemeine Kursprinzipien

**Jedes Thema zuerst an einem generischen Beispiel üben, bevor es auf TeamBoard übertragen wird.**
Das generische Beispiel trennt das neue Konzept von der Komplexität des laufenden Projekts - Fehler lassen sich leichter einem einzelnen neuen Konzept zuordnen.

**Nach jedem Modul einen klaren, überprüfbaren Checkpoint definieren.**
Ein konkretes, beobachtbares Ergebnis (z. B. "`docker ps` zeigt den Container") verhindert, dass Unsicherheit über den erreichten Stand unbemerkt in das nächste Modul mitgenommen wird.

**Copilot-Vorschläge grundsätzlich prüfen, bei sicherheitsrelevantem Code (Modul 16) besonders kritisch.**
Ein unreflektiert übernommener Vorschlag kann bei einfachem UI-Code wenig schaden, bei Authentifizierungslogik aber eine echte Schwachstelle erzeugen.
