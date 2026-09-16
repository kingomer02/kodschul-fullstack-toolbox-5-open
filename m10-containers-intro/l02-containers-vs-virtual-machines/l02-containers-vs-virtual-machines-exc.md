# Lab 10.2 - Übung: Container vs. virtuelle Maschinen

**Dauer:** ca. 15 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - konzeptionelle Übung, keine Codeänderung.

## Ausgangslage

Docker läuft lokal (Lab 10.1).

## Aufgaben

1. Miss die Startzeit eines Containers: `time docker run --rm alpine echo "hello"`.
2. Vergleiche das Ergebnis in der Gruppe mit einer geschätzten VM-Startzeit (aus Erfahrung oder Trainerangabe) und halte den Größenordnungsunterschied schriftlich fest (z. B. Millisekunden vs. Minuten).
3. Skizziere in 2-3 Stichpunkten, welche TeamBoard-Komponenten (Backend, Frontend, MongoDB) später als eigene Container laufen sollen.
4. Beantworte schriftlich: Warum wäre eine gemeinsame VM für alle drei Komponenten hier weniger praktisch als drei separate Container?

## Checkpoint

- Eine dokumentierte Startzeit-Messung aus Aufgabe 1 liegt vor.
- Eine kurze schriftliche Begründung aus Aufgabe 4 liegt vor.

## Abschlusskriterien

- Die Skizze aus Aufgabe 3 benennt mindestens drei separate Komponenten.

## Fallback

Ohne Vergleichswert für VM-Startzeiten: die vom Trainer genannte Beispielzahl übernehmen und den Vergleich darauf stützen.
