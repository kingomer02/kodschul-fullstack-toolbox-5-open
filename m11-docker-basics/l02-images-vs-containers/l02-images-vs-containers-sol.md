# Lab 11.2 - Lösung: Images vs. Container

## Aufgabe 1-2: Images laden und vergleichen

```bash
docker pull node:20
docker pull node:20-alpine
docker images
```

Erwartung: `node:20` liegt bei ca. 1 GB, `node:20-alpine` bei ca. 150-200 MB - ein Unterschied von mehreren hundert MB.

## Aufgabe 3: Zwei Container aus einem Image

```bash
docker run --name c1 -d nginx
docker run --name c2 -d nginx
docker ps
```

Beide erscheinen mit unterschiedlichen Container-IDs, gleichem `IMAGE`-Wert (`nginx`).

## Aufgabe 4: Unabhängige Zustände

```bash
docker exec c1 sh -c "echo hallo > /tmp/test.txt"
docker exec c1 cat /tmp/test.txt
# hallo
docker exec c2 ls /tmp
# test.txt erscheint NICHT in der Liste
```

## Aufgabe 5: Aufräumen

```bash
docker stop c1 c2
docker rm c1 c2
```

## Grenzen

Der Größenunterschied zwischen Debian- und Alpine-basierten Images ist ein Richtwert - genaue Werte ändern sich mit neuen Versionen und sollten am Kurstag mit `docker images` erneut geprüft werden.
