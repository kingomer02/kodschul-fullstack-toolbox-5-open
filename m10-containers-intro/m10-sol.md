# Transfer-Übung Modul 10 - Lösung: Container-Architekturskizze für TeamBoard

## Aufgabe 1-3: Beispielnotiz

```md
# Container-Plan TeamBoard

- Backend (Node/TS): eigener Dockerfile nötig, Basis-Image `node:20-alpine` (klein, offizielles Node-Image).
- MongoDB: fertiges Image `mongo` aus der Registry, kein eigener Dockerfile nötig.
- Offene Fragen: Wie kommt der TypeScript-Build (dist/) ins Image? Multi-Stage-Build nötig? Wie verbinden sich Backend und MongoDB im selben Compose-Netzwerk?
```

## Grenzen

Diese Skizze ist eine Planungsgrundlage - die tatsächliche Umsetzung (Dockerfile, Compose-Datei) folgt in Modul 11-13 und kann von der Skizze abweichen.
