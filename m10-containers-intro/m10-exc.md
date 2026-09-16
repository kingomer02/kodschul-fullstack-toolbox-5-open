# Transfer-Übung Modul 10 - Übung: Container-Architekturskizze für TeamBoard

**Dauer:** ca. 15 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - rein konzeptionelle Vorbereitung, kein Code wird geändert.

## Ziel

Die Begriffe aus den drei Labs (WSL 2, Container vs. VM, Container-Ökosystem) auf TeamBoard konkret anwenden, bevor in Modul 11 tatsächlich ein Dockerfile geschrieben wird.

## Ausgangslage

- Begriffe Image, Container, Registry, Dockerfile, Docker Compose sind aus Lab 10.3 bekannt.
- Der aktuelle TeamBoard-Stand (Node.js/TypeScript-Backend, kein Frontend-Server) ist aus Modul 5-8 bekannt.

## Aufgaben

1. Skizziere in einer kurzen Notiz, welche TeamBoard-Komponenten künftig als eigene Container laufen sollen (mindestens: Backend, MongoDB) und ob dafür ein fertiges Registry-Image oder ein eigener Dockerfile nötig ist (Bezug zu Lab 10.3, Aufgabe 4).
2. Notiere, welches Basis-Image für das Node/TypeScript-Backend sinnvoll erscheint (z. B. `node:20-alpine`) und begründe kurz warum.
3. Halte 2-3 offene Fragen fest, die du dir für Modul 11 (Dockerfile schreiben) merken willst.

## Checkpoint

- Eine kurze lokale Notiz-Datei (z. B. `container-plan.md`) mit den drei Punkten aus den Aufgaben liegt vor.

## Abschlusskriterien

- Du kannst in eigenen Worten erklären, warum TeamBoard ab Modul 11 containerisiert wird - und dass sich dadurch am bereits geschriebenen Backend-Code selbst nichts ändert.

## Fallback

Bei Unsicherheit die Lösungen von Lab 10.1-10.3 sowie `docker-cheatsheet.md` erneut durchgehen, bevor die Notiz geschrieben wird.
