# Transfer-Übung Modul 22 - Lösung: Vollständige Live-Demo des gesamten TeamBoard-Flusses

## Aufgabe 1: Commit-Anzahl

```bash
git log --oneline | wc -l
# Beispiel: 47
```

## Aufgabe 2: Umgebung frisch starten

```bash
docker compose down -v
docker compose up -d --build
docker compose ps
# backend   running
# mongo     running
```

## Aufgabe 3: Frontend starten

```bash
cd frontend
npm run dev
# http://localhost:5173
```

## Aufgabe 4: Kompletter Fluss

```bash
curl -X POST http://localhost:3000/auth/register \
  -H "Content-Type: application/json" -d '{"username": "trainer", "password": "demo1234"}'
```

Im Browser: `trainer`/`demo1234` einloggen → "Abschluss-Demo-Ticket" anlegen → zweimal "Weiter →" klicken → Ticket erscheint in "Done".

## Aufgabe 5: Blick hinter die Kulissen

```bash
docker compose logs backend
```

Zeigt die eingehenden REST-Aufrufe (`/auth/login`, `/tickets`, `/tickets/:id/status`) in der Reihenfolge der Live-Demo.

## Aufgabe 6: Zusammenfassung

Git/GitHub mit CI (Module 1-9) schuf die Grundlage für nachvollziehbare, automatisiert geprüfte Änderungen. Docker/Compose (Module 10-13) verpackte Backend und MongoDB reproduzierbar. REST und GraphQL über MongoDB (Module 14-15) stellten die Ticket-Daten bereit, JWT-Auth (Modul 16) sicherte sie ab. Die React-SPA mit Bootstrap/Sass (Module 17-19) machte das gesamte System für Nutzende bedienbar - vom ersten Login bis zum fertig bewegten Ticket.

## Grenzen

Diese Demo zeigt den "glücklichen Pfad" vollständig - einzelne Fehlerfälle (falsches Passwort, abgelaufener Token) wurden bereits separat in Modul 16 und 19 geprüft und sind hier bewusst nicht wiederholt.
