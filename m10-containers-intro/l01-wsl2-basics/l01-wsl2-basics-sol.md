# Lab 10.1 - Lösung: WSL 2-Grundlagen

## Aufgabe 1: Version prüfen

```bash
docker --version
# Docker version 25.x.x, build ...
```

## Aufgabe 2: `docker info` lesen

```bash
docker info
```

Relevante Zeile (Beispiel):

```text
Containers: 0
 Running: 0
 Paused: 0
 Stopped: 0
```

## Aufgabe 3: Testcontainer starten

```bash
docker run hello-world
```

Die Ausgabe erklärt in Kurzform, dass der Docker-Client das Image angefragt, der Daemon es (falls nötig) heruntergeladen und einen Container daraus gestartet hat.

## Aufgabe 4: WSL-Integration prüfen (Windows)

Docker Desktop -> Settings -> Resources -> WSL Integration: die verwendete Distribution (z. B. `Ubuntu`) muss aktiviert sein.

## Grenzen

`hello-world` demonstriert nur, dass Docker grundsätzlich funktioniert - der Unterschied zwischen Container und VM wird in Lab 10.2 vertieft.
