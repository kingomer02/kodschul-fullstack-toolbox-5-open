# Transfer-Übung Modul 22 - Übung: Vollständige Live-Demo des gesamten TeamBoard-Flusses

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - abschließende Gesamt-Demo des bestehenden Projekts, ohne Code zu ändern.

## Ziel

Den gesamten TeamBoard-Kurs in einer einzigen, zusammenhängenden Demonstration zusammenführen: von der Git-Historie über die Container-Infrastruktur bis zur abgesicherten React-Oberfläche - als krönender Abschluss des Kurses.

## Ausgangslage

- Der vollständige TeamBoard-Stand aus Modul 19 liegt vor; Docker-Umgebung ist einsatzbereit.

## Aufgaben

1. Zeige mit `git log --oneline | wc -l` die Gesamtzahl der Commits über den gesamten Kurs.
2. Starte die komplette Umgebung frisch: `docker compose down -v` gefolgt von `docker compose up -d --build`.
3. Starte das Frontend (`npm run dev` im `frontend/`-Ordner).
4. Führe den kompletten funktionalen Fluss einmal live durch: registrieren (per `curl`, da keine Registrierungsoberfläche existiert), im Browser einloggen, ein Ticket anlegen, es zweimal weiterbewegen bis "Done".
5. Zeige parallel `docker compose logs backend` oder die GraphQL-Playground-Oberfläche als "Blick hinter die Kulissen".
6. Fasse in 3-4 Sätzen die komplette Kette zusammen: Git/GitHub mit CI → Docker/Compose → REST+GraphQL/MongoDB → JWT-Auth → React-SPA.

## Checkpoint

- Der komplette Fluss (Login → Ticket anlegen → zweimal weiterbewegen → "Done") läuft in der Live-Demo ohne Fehler durch.
- Sowohl die Oberfläche als auch die Backend-Logs zeigen konsistent denselben Endzustand.

## Abschlusskriterien

- Die Zusammenfassung aus Aufgabe 6 nennt alle fünf Stationen der Kette in der richtigen Reihenfolge.

## Lösungshinweise

```bash
git log --oneline | wc -l

docker compose down -v
docker compose up -d --build

cd frontend && npm run dev
```

```bash
curl -X POST http://localhost:3000/auth/register \
  -H "Content-Type: application/json" -d '{"username": "trainer", "password": "demo1234"}'
```

Im Browser: einloggen, Ticket anlegen, zweimal "Weiter →" klicken.

```bash
docker compose logs backend
```

Zusammenfassung: Git/GitHub mit CI (Module 1-9) legte die Grundlage; Docker/Compose (Module 10-13) containerisierte Backend und MongoDB; REST/GraphQL über MongoDB (Module 14-15) und JWT-Auth (Modul 16) sicherten die Daten ab; die React-SPA (Module 17-19) machte all das für Nutzende sichtbar und bedienbar.

## Fallback

Falls die Umgebung nach `docker compose down -v` länger zum Neustarten braucht: den Docker-Layer-Cache aus Modul 12 nutzen - ein erneuter Build sollte trotzdem deutlich schneller sein als der allererste Build im Kurs.
