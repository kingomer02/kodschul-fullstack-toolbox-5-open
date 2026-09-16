# Docker/Container-Cheatsheet

Schnellreferenz für Modul 10 (WSL 2, Container vs. VM, Ökosystem) - vertiefende Befehle folgen in Modul 11-13.

## Umgebung prüfen

| Befehl                   | Wirkung                                         |
| ------------------------ | ----------------------------------------------- |
| `docker --version`       | installierte Docker-Version anzeigen            |
| `docker info`            | Details zur laufenden Docker-Engine anzeigen    |
| `docker run hello-world` | Testcontainer starten, Grundfunktion bestätigen |

## Images

| Befehl                 | Wirkung                                  |
| ---------------------- | ---------------------------------------- |
| `docker search <name>` | öffentliche Images auf Docker Hub suchen |
| `docker pull <image>`  | Image aus einer Registry herunterladen   |
| `docker images`        | lokal vorhandene Images auflisten        |
| `docker rmi <image>`   | lokales Image löschen                    |

## Container

| Befehl                    | Wirkung                                                  |
| ------------------------- | -------------------------------------------------------- |
| `docker run <image>`      | Container aus einem Image starten                        |
| `docker run --rm <image>` | Container starten und nach Beenden automatisch entfernen |
| `docker ps`               | laufende Container auflisten                             |
| `docker ps -a`            | alle Container auflisten (auch gestoppte)                |
| `docker stop <container>` | laufenden Container stoppen                              |
| `docker rm <container>`   | gestoppten Container entfernen                           |

## Zentrale Begriffe

| Begriff        | Bedeutung                                                             |
| -------------- | --------------------------------------------------------------------- |
| Image          | unveränderliche Vorlage für Container                                 |
| Container      | laufende Instanz eines Images                                         |
| Registry       | Speicherort für Images (z. B. Docker Hub)                             |
| Dockerfile     | Bauanleitung zum Erzeugen eines eigenen Images (ab Modul 12)          |
| Docker Compose | mehrere zusammengehörige Container gemeinsam definieren (ab Modul 13) |

## Container vs. VM

| Merkmal          | Container              | VM                  |
| ---------------- | ---------------------- | ------------------- |
| Kernel           | geteilt mit Host       | eigener Gast-Kernel |
| Startzeit        | Millisekunden-Sekunden | Sekunden-Minuten    |
| Ressourcenbedarf | gering                 | hoch                |

## Faustregeln

- `docker ps` zuerst ausführen, wenn ein Container "nicht erreichbar" scheint - läuft er überhaupt?
- `--rm` bei kurzlebigen Testcontainern verwenden, um aufzuräumen.
- Fertige, offizielle Images (z. B. `mongo`, `nginx`) bevorzugen, statt sie unnötig selbst nachzubauen.
