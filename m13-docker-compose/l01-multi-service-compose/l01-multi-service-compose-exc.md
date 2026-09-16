# Lab 13.1 - Übung: Mehrere Services verbinden

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - eigenständiges Beispiel mit fremden Images.

## Vorbereitung

- Ein leerer Ordner `sample-compose/` liegt lokal bereit.

## Aufgaben

1. Lege `sample-compose/docker-compose.yml` mit zwei Services an: `cache` (Image `redis:7-alpine`) und `app` (Image `alpine`), wobei `app` per `command` einen `redis-cli -h cache ping` gegen `cache` ausführt.
2. Ergänze `depends_on: [cache]` bei `app`.
3. Starte beide Services: `docker compose -f sample-compose/docker-compose.yml up`.
4. Beobachte die Ausgabe des `app`-Containers und beende danach mit `Strg+C`, anschließend `docker compose -f sample-compose/docker-compose.yml down`.

## Checkpoint

- Der `app`-Container gibt `PONG` aus.

## Abschlusskriterien

- Du kannst erklären, warum `-h cache` (Servicename) funktioniert, obwohl keine IP-Adresse angegeben wurde.

## Fallback

Falls `docker compose` (ohne Bindestrich) nicht erkannt wird: die ältere Standalone-Variante `docker-compose` (mit Bindestrich) verwenden - Funktionsweise ist für diesen Kurs identisch.
