# Lab 10.1 - Übung: WSL 2-Grundlagen

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - reine Verifikation der lokalen Umgebung.

## Ausgangslage

Docker Desktop ist laut Vorbereitungshinweisen installiert (unter Windows mit WSL 2-Backend).

## Aufgaben

1. Prüfe mit `docker --version`, dass Docker installiert ist.
2. Führe `docker info` aus und identifiziere darin die Zeile, die die Anzahl laufender Container zeigt.
3. Führe `docker run hello-world` aus und lies die Ausgabetext-Erklärung, was gerade passiert ist.
4. (Nur unter Windows) Prüfe in Docker Desktop unter "Settings -> Resources -> WSL Integration", dass WSL 2 als Backend aktiv ist.

## Checkpoint

- `docker run hello-world` gibt die offizielle Bestätigungsmeldung aus, ohne Fehler.

## Abschlusskriterien

- `docker info` liefert plausible Werte (keine Verbindungsfehler zum Docker-Daemon).

## Fallback

Bei nicht funktionierendem lokalem Docker-Setup: das vom Trainer bereitgestellte Referenz-Setup (z. B. Cloud-Terminal mit Docker) für die restlichen Docker-Module nutzen und das lokale Setup parallel zur Pause reparieren.
