# Lab 10.3 - Übung: Überblick über das Container-Ökosystem

**Dauer:** ca. 15 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - konzeptionelle Übung.

## Ausgangslage

Docker läuft lokal (Lab 10.1); die Begriffe aus dem Lab-Text liegen vor.

## Aufgaben

1. Ordne folgenden fünf Begriffen in eigenen Worten (1 Satz je Begriff) zu: Image, Container, Registry, Dockerfile, Docker Compose.
2. Finde mit `docker search nginx` (oder auf hub.docker.com) drei verschiedene öffentliche Images und notiere ihre Namen.
3. Ziehe eines der gefundenen Images lokal: `docker pull nginx` und liste danach lokale Images mit `docker images`.
4. Beantworte schriftlich: Welche der TeamBoard-Komponenten (Backend, Frontend, MongoDB) wird voraussichtlich ein offizielles, fertiges Image von der Registry nutzen, welche einen selbst geschriebenen Dockerfile-basierten Build brauchen?

## Checkpoint

- Fünf korrekt zugeordnete Begriffserklärungen liegen vor.
- `docker images` zeigt das per `docker pull` geladene Image.

## Abschlusskriterien

- Aufgabe 4 unterscheidet klar zwischen "fertiges Image aus der Registry" (z. B. MongoDB) und "eigenes Dockerfile" (z. B. Backend).

## Fallback

Ohne Internetzugriff für `docker search`: die vom Trainer vorbereitete Liste bekannter Images (z. B. `nginx`, `mongo`, `node`) als Ausgangspunkt für Aufgabe 2 verwenden.
