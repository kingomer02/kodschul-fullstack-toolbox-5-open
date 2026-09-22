# Transfer-Übung Modul 13 - Übung: Day-3-Meilenstein bestätigen

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - prüft nur den bestehenden Compose-Stand, ändert keinen Code.

## Ziel

Bestätigen, dass Backend und MongoDB als vollständiger, gemeinsam startbarer Stand funktionieren - der Tag-3-Meilenstein vor den API-Themen ab Modul 14.

## Ausgangslage

- `docker-compose.yml` (Lab 13.2) und der erweiterte CI-Workflow (Lab 13.3) liegen auf `main`.

## Aufgaben

1. Führe einen vollständigen, sauberen Durchlauf aus: `docker compose down -v` (falls noch Reste laufen), dann `docker compose up -d --build`.
2. Prüfe mit `docker compose ps -a`, dass `mongo` läuft und `backend` mit `Exited (0)` sauber durchgelaufen ist, und mit `docker compose logs backend`, dass die gewohnte Ausgabe ohne Fehler erscheint.
3. Prüfe erneut die Netzwerk-Erreichbarkeit von `mongo` aus `backend` (wie in Lab 13.2).
4. Fahre alles sauber herunter: `docker compose down`.
5. Halte in einem Satz fest, was noch fehlt, damit das Backend MongoDB tatsächlich nutzt (Vorschau auf Modul 15).

## Checkpoint

- Ein kompletter `down -v` → `up -d --build` → `down`-Zyklus läuft ohne manuelle Nacharbeit durch.

## Abschlusskriterien

- Der Tag-3-Stand (containerisiertes Backend + MongoDB, CI validiert die Compose-Datei) ist reproduzierbar und bereit für die REST-API in Modul 14.

## Lösungshinweise

```bash
docker compose down -v
docker compose up -d --build
docker compose ps
docker compose logs backend
docker compose run --rm --entrypoint sh backend -c "getent hosts mongo"
docker compose down
```

Fehlend für echte Nutzung: MongoDB-Treiber (z. B. `mongodb`-Paket) im Backend installieren und `MONGO_URL` tatsächlich zum Verbindungsaufbau verwenden - das übernimmt Modul 15.

## Fallback

Falls `--build` sehr lange dauert: prüfen, ob der Docker-Layer-Cache aus Modul 12 durch eine vorherige `docker system prune` versehentlich gelöscht wurde.
