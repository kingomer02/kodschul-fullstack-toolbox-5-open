# Node.js-Cheatsheet

Schnellreferenz für die in Modul 5 (Grundlagen/Installation) verwendeten Befehle.

## Version und Umgebung prüfen

| Befehl           | Wirkung                               |
| ---------------- | ------------------------------------- |
| `node --version` | installierte Node.js-Version anzeigen |
| `npm --version`  | installierte NPM-Version anzeigen     |
| `node`           | interaktive Node-REPL starten         |

## Skripte ausführen

| Befehl             | Wirkung                                     |
| ------------------ | ------------------------------------------- |
| `node <datei>.js`  | JavaScript-Datei mit Node.js ausführen      |
| `node -e "<code>"` | Code-Schnipsel direkt ausführen, ohne Datei |

## Nützliche globale Objekte

| Objekt/Property    | Zweck                                            |
| ------------------ | ------------------------------------------------ |
| `process.version`  | aktuelle Node-Version im Skript                  |
| `process.platform` | Betriebssystem (`darwin`, `win32`, `linux`)      |
| `process.argv`     | an das Skript übergebene Kommandozeilenargumente |
| `process.env`      | Umgebungsvariablen                               |

## Browser-JS vs. Node.js

| Merkmal                          | Browser                      | Node.js                          |
| -------------------------------- | ---------------------------- | -------------------------------- |
| DOM/Window                       | vorhanden                    | nicht vorhanden                  |
| Dateisystemzugriff               | nicht direkt möglich         | über `fs`-Modul möglich          |
| Typischer Einsatz in diesem Kurs | React-Frontend (Modul 18-19) | Backend/Build-Tools (ab Modul 6) |

## Faustregeln

- Node.js läuft single-threaded mit einer Event-Loop - blockierende Operationen möglichst vermeiden.
- Für I/O (Datei, Netzwerk) asynchrone APIs (Callbacks/Promises/`async`/`await`) bevorzugen.
