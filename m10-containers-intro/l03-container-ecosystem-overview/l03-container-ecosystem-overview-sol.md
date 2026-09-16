# Lab 10.3 - Lösung: Überblick über das Container-Ökosystem

## Aufgabe 1: Begriffe zuordnen

- **Image:** unveränderliche Vorlage, aus der Container gestartet werden.
- **Container:** eine laufende (oder gestoppte) Instanz eines Images.
- **Registry:** Speicherort, von dem Images heruntergeladen oder dorthin hochgeladen werden (z. B. Docker Hub).
- **Dockerfile:** Textdatei mit Bauanleitung, aus der ein eigenes Image gebaut wird.
- **Docker Compose:** Werkzeug/Datei, um mehrere zusammengehörige Container gemeinsam zu definieren und zu starten.

## Aufgabe 2-3: Images suchen und ziehen

```bash
docker search nginx
docker pull nginx
docker images
```

Beispielausgabe von `docker images`:

```text
REPOSITORY   TAG       IMAGE ID       SIZE
nginx        latest    <id>           187MB
```

## Aufgabe 4: Fertiges Image vs. eigener Dockerfile

- **MongoDB:** nutzt voraussichtlich das offizielle `mongo`-Image direkt aus der Registry, ohne eigenen Dockerfile.
- **Backend (Node/Express):** braucht einen eigenen Dockerfile, da eigener Anwendungscode (TeamBoard-spezifisch) enthalten sein muss.
- **Frontend:** je nach Stand entweder ein einfaches statisches Image oder ebenfalls ein eigener Dockerfile-Build (abhängig vom Stand ab Modul 17/18).

## Grenzen

Diese Einschätzung wird in Modul 11-13 praktisch überprüft, wenn Backend und MongoDB tatsächlich per Docker/Compose verbunden werden.
