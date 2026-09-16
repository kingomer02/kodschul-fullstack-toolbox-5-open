# Lab 11.1 - Lösung: Docker-CLI-Grundlagen

## Aufgabe 1-2: Container starten und Startseite prüfen

```bash
docker run --name lab11-nginx -d -p 8080:80 nginx
```

`http://localhost:8080` zeigt die Standard-nginx-Willkommensseite ("Welcome to nginx!").

## Aufgabe 3: Logs ansehen

```bash
docker logs lab11-nginx
```

Erwartete Ausgabe: mindestens eine Zeile im nginx-Access-Log-Format mit Statuscode `200` für `GET /`.

## Aufgabe 4: Shell im Container

```bash
docker exec -it lab11-nginx sh
ls /usr/share/nginx/html
# index.html  50x.html
exit
```

## Aufgabe 5-6: Aufräumen

```bash
docker stop lab11-nginx
docker rm lab11-nginx
docker ps -a
# lab11-nginx erscheint nicht mehr in der Liste
```

## Grenzen

`docker rm` ohne vorheriges `stop` schlägt bei einem laufenden Container fehl (Fehlermeldung "container is running") - das ist beabsichtigtes Schutzverhalten.
