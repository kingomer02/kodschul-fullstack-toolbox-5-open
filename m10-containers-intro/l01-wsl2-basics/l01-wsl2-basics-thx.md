# Modul 10: Einführung in Container

## Lab 10.1 - WSL 2-Grundlagen

---

## Lab-Ziel

Du verstehst, welche Rolle WSL 2 unter Windows für Docker spielt, und hast deine Docker-Umgebung verifiziert.

**Leitfragen:**

<details>
<summary>Was ist WSL 2?</summary>

Windows Subsystem for Linux Version 2 - eine echte Linux-Kernel-Umgebung innerhalb von Windows, auf der u. a. Docker Desktop unter Windows aufsetzt.

</details>

<details>
<summary>Warum braucht Docker Desktop unter Windows überhaupt WSL 2?</summary>

Container nutzen Linux-Kernel-Funktionen (Namespaces, Cgroups); WSL 2 stellt diese Grundlage nativ und performant bereit, statt eine vollständige klassische VM zu benötigen.

</details>

<details>
<summary>Was zeigt `docker info`, und wozu ist es beim Fehlersuchen nützlich?</summary>

Es zeigt Details zur laufenden Docker-Engine (u. a. Betriebssystem, Kernel-Version, Anzahl Container/Images) - ein guter erster Schritt, um zu prüfen, ob Docker überhaupt korrekt läuft.

</details>

---

## WSL 2 einordnen

- **Ohne WSL 2 (macOS/Linux):** Docker Desktop nutzt die native Virtualisierung des Betriebssystems bzw. läuft direkt auf dem Linux-Kernel.
- **Mit WSL 2 (Windows):** Docker Desktop nutzt eine leichtgewichtige Linux-VM (WSL 2), statt eine klassische, schwergewichtige virtuelle Maschine zu benötigen.

**Grenze:** dieser Kurs behandelt WSL 2 als Voraussetzung, nicht als eigenständiges Lernthema - Details zur WSL-Konfiguration sind trainerseitig vorbereitet.

---

## Docker-Umgebung verifizieren

```bash
docker --version
docker info
docker run hello-world
```

- `docker run hello-world` lädt ein minimales Test-Image und bestätigt, dass Container tatsächlich gestartet werden können.

---

## Checkpoint

`docker run hello-world` läuft ohne Fehler und gibt die Bestätigungsmeldung von Docker aus.

Weiter geht es mit Lab 10.2: Container vs. virtuelle Maschinen.
