# Lab 10.2 - Lösung: Container vs. virtuelle Maschinen

## Aufgabe 1: Startzeit messen

```bash
time docker run --rm alpine echo "hello"
# real    0m0.612s (Beispielwert, abhängig vom lokalen Setup)
```

## Aufgabe 2: Vergleich

Eine typische VM (z. B. via VirtualBox) benötigt eher 30-90 Sekunden zum vollständigen Hochfahren eines Gastbetriebssystems - Größenordnung Sekunden bis Minuten gegenüber Millisekunden bis Sekunden bei Containern.

## Aufgabe 3: TeamBoard-Komponenten als Container

- Backend (Node.js/Express-API)
- MongoDB (Datenbank)
- Frontend (statisch oder später React-Build)

## Aufgabe 4: Begründung

Getrennte Container erlauben es, jede Komponente unabhängig neu zu starten, zu skalieren oder auszutauschen (z. B. MongoDB-Version wechseln), ohne die anderen Komponenten anzufassen - eine gemeinsame VM würde diese Trennung nicht von sich aus bieten und wäre beim Neustart insgesamt langsamer.

## Grenzen

Die gemessene Startzeit hängt stark vom lokalen Rechner und Cache-Zustand ab - der Vergleich ist als Größenordnung, nicht als exakte Benchmarkzahl zu verstehen.
