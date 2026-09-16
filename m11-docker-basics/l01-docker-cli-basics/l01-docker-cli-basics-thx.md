# Modul 11: Docker-Grundlagen

## Lab 11.1 - Docker-CLI-Grundlagen

---

## Lab-Ziel

Du kannst mit den grundlegenden Docker-CLI-Befehlen ein fremdes Image starten, untersuchen und wieder sauber aufräumen.

**Leitfragen:**

<details>
<summary>Was ist der Unterschied zwischen `docker run` und `docker start`?</summary>

`docker run` erstellt einen neuen Container aus einem Image und startet ihn; `docker start` startet einen bereits existierenden, gestoppten Container erneut.

</details>

<details>
<summary>Wie siehst du laufende und gestoppte Container gleichzeitig?</summary>

Mit `docker ps -a` (ohne `-a` zeigt `docker ps` nur laufende Container).

</details>

<details>
<summary>Wozu dient `docker exec`?</summary>

Um einen Befehl (z. B. eine Shell) in einem bereits laufenden Container auszuführen, ohne einen neuen Container zu starten.

</details>

---

## Die wichtigsten CLI-Befehle

| Befehl                           | Zweck                                                 |
| -------------------------------- | ----------------------------------------------------- |
| `docker run <image>`             | Container aus einem Image erstellen und starten       |
| `docker ps` / `docker ps -a`     | laufende / alle Container auflisten                   |
| `docker logs <container>`        | Konsolenausgabe eines Containers ansehen              |
| `docker exec -it <container> sh` | interaktive Shell in einem laufenden Container öffnen |
| `docker stop <container>`        | Container sauber anhalten                             |
| `docker rm <container>`          | gestoppten Container entfernen                        |

**Grenze:** `docker rm -f` erzwingt das Entfernen eines laufenden Containers - im Kursverlauf immer erst `stop`, dann `rm` verwenden, um Zustände bewusst zu beobachten.

---

## Container benennen und wiederfinden

```bash
docker run --name mein-nginx -d nginx
docker ps
docker logs mein-nginx
```

- `--name` vergibt einen sprechenden Namen statt der zufälligen Docker-ID.
- `-d` (detached) startet den Container im Hintergrund, die Shell bleibt frei.

---

## Checkpoint

`docker ps -a` zeigt einen benannten Container, `docker logs` liefert dessen Ausgabe, `docker exec -it ... sh` öffnet erfolgreich eine Shell darin.

Weiter geht es mit Lab 11.2: Images vs. Container im Detail.
