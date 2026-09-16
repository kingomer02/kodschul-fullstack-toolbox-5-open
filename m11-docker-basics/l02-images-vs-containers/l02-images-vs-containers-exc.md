# Lab 11.2 - Übung: Images vs. Container

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - Diagnose-Übung mit fremden Images.

## Aufgaben

1. Lade zwei Varianten desselben Images: `docker pull node:20` und `docker pull node:20-alpine`.
2. Vergleiche die Größen mit `docker images` und notiere den Größenunterschied.
3. Starte zwei benannte Container aus demselben Image: `docker run --name c1 -d nginx` und `docker run --name c2 -d nginx`.
4. Erzeuge in `c1` eine Testdatei: `docker exec c1 sh -c "echo hallo > /tmp/test.txt"`. Prüfe danach mit `docker exec c2 ls /tmp`, dass die Datei dort **nicht** existiert.
5. Räume auf: stoppe und entferne `c1` und `c2`.

## Checkpoint

- `docker images` zeigt eine deutlich kleinere Größe für `node:20-alpine` als für `node:20`.
- Die Testdatei existiert nur in `c1`, nicht in `c2`.

## Abschlusskriterien

- Du kannst in einem Satz erklären, warum dieselbe Grundlage (Image) zu unabhängigen Zuständen (Container) führt.

## Fallback

Falls der Download der Images wegen Netzwerkbeschränkungen fehlschlägt: die Größenangaben von Docker Hub (hub.docker.com, Tags-Ansicht von `node`) als Referenz nutzen, statt lokal zu vergleichen.
