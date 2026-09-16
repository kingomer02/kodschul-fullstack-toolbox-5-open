# FAQ: Fullstack Developer Toolbox

## Organisatorisches

**Muss ich vor Kursbeginn etwas installieren?**
Ja: VS Code, Node.js, Git, Docker Desktop sowie unter Windows WSL 2. Der Installationscheck findet direkt zu Kursbeginn an Tag 1 statt, damit technische Probleme nicht in die eigentlichen Inhalte hineinlaufen.

**Was passiert, wenn eine Installation am Kurstag nicht funktioniert?**
Der Tag-1-Puffer von rund 20 Minuten ist genau dafür vorgesehen. Bei tieferliegenden Problemen (z. B. Docker Desktop unter Windows ohne funktionierendes WSL 2) hilft der Trainer individuell, während die zweite Person bereits weiterarbeitet.

**Warum ist die Gruppe auf maximal 2 Personen begrenzt?**
Bei dieser Größe ist individuelles Tempo möglich, ohne dass ein separates Grund-/Vertiefungs-Angebot nötig wird. Trotzdem gibt es an Tag 1 und Tag 2 Pufferzeiten, falls die TypeScript-/JavaScript-Vorkenntnisse unterschiedlich tief sind.

**Muss ich mich zu Kursbeginn vorstellen?**
Ja, kurz: Name, Rolle, fachlicher Hintergrund, Organisation, bisherige Erfahrung mit den Kursthemen, Erwartungen und ein konkretes Einsatzszenario. Persönliche Details wie Stadt oder Wetter sind optional.

## Zum Kursprojekt TeamBoard

**Was genau ist TeamBoard?**
Ein minimales Kanban-Ticketsystem: Tickets mit Titel, Beschreibung, zugewiesener Person und Status (To Do/In Progress/Done). Es ist bewusst einfach gehalten, damit an jedem Kurstag genug Zeit für das jeweilige Werkzeug-Thema bleibt.

**Baut wirklich jedes Modul auf TeamBoard auf?**
Fast jedes - Ausnahmen sind Modul 9 (reiner Puffer ohne neuen Projektschritt) sowie Modul 20 und 21 (Trainer-Demos zu Angular und Azure, ohne eigene Übung am Projekt). Modul 22 ist ein Rückblick statt eines neuen Schritts.

**Was, wenn ich in einem früheren Modul nicht fertig geworden bin?**
Jedes Modul endet mit einem konkreten Checkpoint. Wird dieser nicht erreicht, stellt der Trainer für das nächste Modul einen funktionierenden Zwischenstand bereit, damit der Anschluss an die Gruppe nicht verloren geht.

**Warum wird jedes Thema zuerst generisch geübt und erst danach an TeamBoard angewendet?**
So lässt sich ein neues Konzept (z. B. Generics oder JWT) isoliert verstehen, bevor es in der Komplexität des laufenden Projekts angewendet wird. Fehler lassen sich dadurch leichter einer Ursache zuordnen.

## Technische Themen

**Warum wird schon an Tag 1 eine CI-Pipeline eingerichtet, bevor überhaupt viel Code existiert?**
Damit ab diesem Zeitpunkt jede weitere Änderung sofort automatisch geprüft wird. Ein früher eingerichteter, noch einfacher CI-Lauf ist leichter zu verstehen als eine nachträglich in ein bereits komplexes Projekt eingebaute Pipeline.

**Warum wird ab Modul 10 alles containerisiert weiterentwickelt?**
Das ist eine bewusste, im Kurs dokumentierte Trainer-Entscheidung: Sobald Docker beherrscht wird, spiegelt die Entwicklungsumgebung von da an eine reale, produktionsnahe Umgebung wider. Alle Module ab Tag 3 setzen ein funktionierendes Docker-Desktop-Setup voraus.

**Warum gibt es sowohl REST als auch GraphQL im selben Projekt?**
Damit beide Ansätze direkt am selben Datenmodell verglichen werden können, statt sie nur theoretisch gegenüberzustellen. Beide APIs greifen auf dieselbe Datenhaltung (Repository) zu.

**Warum wird MongoDB statt einer relationalen Datenbank verwendet?**
MongoDB passt gut zum dokumentenähnlichen Ticket-Datenmodell und wird direkt im Zusammenhang mit dem SQL-vs-NoSQL-Vergleich in Modul 15 eingeführt.

**Was genau macht JWT in diesem Projekt?**
Nach einem erfolgreichen Login stellt der Server ein signiertes Token aus. Das Frontend sendet dieses Token bei jeder weiteren Anfrage mit, sodass geschützte Routen (z. B. Ticket ändern) ohne erneuten Login erreichbar bleiben, aber nicht ohne gültiges Token.

**Warum werden Passwörter gehasht statt verschlüsselt gespeichert?**
Hashing ist bewusst nicht umkehrbar. Selbst bei einem Datenbank-Leck lässt sich aus dem gespeicherten Wert kein Passwort zurückgewinnen - anders als bei einer (theoretisch entschlüsselbaren) Verschlüsselung.

**Warum wird CORS im Kurs eher offen konfiguriert?**
Für die Lernumgebung reicht das aus, um Frontend und Backend unkompliziert miteinander sprechen zu lassen. In einer echten Produktionsumgebung sollte CORS auf konkrete, bekannte Ursprünge eingeschränkt werden - das wird im Kurs als Hinweis mitgegeben.

**Warum werden Angular und Azure nur als Trainer-Demo behandelt und nicht selbst geübt?**
Die Kurszeit reicht nicht aus, um React, Angular und ein volles Cloud-Deployment alle praktisch zu üben. Angular und Azure Static Web Apps werden daher bewusst als Konzept-Demonstration gezeigt, damit die Teilnehmenden die Alternativen zumindest einordnen können.

**Was ist der Unterschied zwischen `useState` und `useEffect`?**
`useState` verwaltet einen veränderlichen Wert innerhalb einer Komponente (z. B. den Inhalt eines Eingabefelds). `useEffect` führt eine Aktion als Reaktion auf ein Ereignis aus, etwa das Nachladen von Tickets, wenn sich das Login-Token ändert.

**Warum wird beim Frontend-Styling sowohl Bootstrap als auch Sass eingesetzt?**
Bootstrap liefert getestete, responsive Grundbausteine; Sass ergänzt gezielt projektspezifische Anpassungen (z. B. Statusfarben für Tickets), ohne alle Grundlagen selbst neu schreiben zu müssen.

## Nach dem Kurs

**Was kann ich nach dem Kurs mit dem Projekt anfangen?**
Laut Kursversprechen könnt ihr das containerisierte Fullstack-TypeScript-Projekt eigenständig erweitern oder warten - inklusive API, Datenbank, SPA-Frontend, CI und Authentifizierung.

**Wo finde ich eine Übersicht aller verwendeten Fachbegriffe?**
Im [Glossar](glossary.md) dieses Moduls, sortiert in der Reihenfolge des Auftretens im Kurs.

**Wo finde ich eine reine Themenliste ohne Erklärungen?**
In [topics.md](topics.md) - eine verschachtelte Liste aller Module und Labs.
