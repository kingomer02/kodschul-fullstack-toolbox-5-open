# Lab 11.1 - Übung: Docker-CLI-Grundlagen

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - Übung mit einem fremden Beispiel-Image.

## Ausgangslage

Docker Desktop läuft (verifiziert in Modul 10).

## Aufgaben

1. Starte einen benannten, im Hintergrund laufenden Container aus dem Image `nginx`: `docker run --name lab11-nginx -d -p 8080:80 nginx`.
2. Öffne `http://localhost:8080` im Browser und prüfe, dass die nginx-Startseite erscheint.
3. Sieh dir mit `docker logs lab11-nginx` die Zugriffs-Logs an, nachdem du die Seite neu geladen hast.
4. Öffne mit `docker exec -it lab11-nginx sh` eine Shell im Container und liste mit `ls /usr/share/nginx/html` die ausgelieferten Dateien auf. Verlasse die Shell mit `exit`.
5. Stoppe und entferne den Container: `docker stop lab11-nginx` gefolgt von `docker rm lab11-nginx`.
6. Prüfe mit `docker ps -a`, dass der Container nicht mehr aufgelistet wird.

## Checkpoint

- Die nginx-Startseite war unter `http://localhost:8080` erreichbar.
- `docker logs` zeigte mindestens einen Zugriffseintrag für den Seitenaufruf.

## Abschlusskriterien

- Der Container wurde sauber gestoppt und entfernt; `docker ps -a` zeigt ihn nicht mehr.

## Fallback

Falls Port 8080 bereits belegt ist: einen anderen Host-Port verwenden, z. B. `-p 8081:80`, und die URL entsprechend anpassen.
