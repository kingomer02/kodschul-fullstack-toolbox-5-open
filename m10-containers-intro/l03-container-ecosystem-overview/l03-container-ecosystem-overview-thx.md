# Modul 10: Einführung in Container

## Lab 10.3 - Überblick über das Container-Ökosystem

---

## Lab-Ziel

Du kennst die wichtigsten Begriffe und Werkzeuge rund um Container und ordnest ein, was in diesem Kurs behandelt wird und was nicht.

**Leitfragen:**

<details>
<summary>Was ist der Unterschied zwischen einem Image und einem Container?</summary>

Ein Image ist eine unveränderliche Vorlage (Dateisystem-Snapshot plus Metadaten); ein Container ist eine laufende (oder gestoppte) Instanz davon.

</details>

<details>
<summary>Was ist eine Container-Registry, und wofür wird sie gebraucht?</summary>

Ein Speicherort für Images (z. B. Docker Hub) - von dort werden Images heruntergeladen (`docker pull`) oder dorthin hochgeladen (`docker push`).

</details>

<details>
<summary>Was ist Kubernetes, und warum wird es in diesem Kurs nicht behandelt?</summary>

Ein Orchestrierungssystem für viele Container über mehrere Maschinen hinweg; für TeamBoard genügt lokal Docker Compose (Modul 13) - Kubernetes ist ein eigenständiges, deutlich umfangreicheres Thema.

</details>

---

## Zentrale Begriffe

| Begriff                           | Bedeutung                                                            |
| --------------------------------- | -------------------------------------------------------------------- |
| Image                             | unveränderliche Vorlage für Container                                |
| Container                         | laufende Instanz eines Images                                        |
| Registry                          | Speicherort für Images (z. B. Docker Hub)                            |
| Dockerfile                        | Bauanleitung zum Erzeugen eines Images                               |
| Docker Compose                    | Werkzeug zum Definieren/Starten mehrerer zusammengehöriger Container |
| Orchestrierung (z. B. Kubernetes) | Verwaltung vieler Container über mehrere Maschinen/Cluster           |

---

## Was dieser Kurs abdeckt - und was nicht

- **Abgedeckt:** Docker CLI, Dockerfiles, Docker Compose (Module 11-13) - ausreichend, um TeamBoard lokal containerisiert laufen zu lassen.
- **Nicht abgedeckt:** Kubernetes, Cloud-Container-Orchestrierung, Multi-Host-Netzwerke - das sind eigenständige, produktionsnahe Themen jenseits dieses Kurses.

**Grenze:** dieser Überblick ordnet nur ein, wo die Kursinhalte im größeren Ökosystem stehen - er ersetzt keine vertiefte Kubernetes-Schulung.

---

## Checkpoint

Die Begriffe Image, Container, Registry, Dockerfile und Compose wurden korrekt einander zugeordnet; die Kursgrenze (kein Kubernetes) ist klar.

Weiter geht es mit Modul 11: Docker-CLI-Grundlagen.
