# Lab 16.3 - Übung: Geschützte Routen testen

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - sichert alle `/tickets`-Routen mit der Auth-Middleware ab.

## Ausgangslage

- `requireAuth`-Middleware (Lab 16.2) existiert, wird aber noch nirgends eingesetzt; `/auth/register` und `/auth/login` funktionieren.

## Aufgaben

1. Registriere in `index.ts` `app.use("/tickets", requireAuth)` **vor** allen bestehenden `/tickets`-Routen.
2. Baue neu und starte: `docker compose up -d --build`.
3. Teste `GET /tickets` **ohne** `Authorization`-Header - erwarte `401`.
4. Registriere (falls noch nicht geschehen) und logge einen Nutzer ein, um einen Token zu erhalten.
5. Teste `GET /tickets`, `POST /tickets` und `PATCH /tickets/:id/status` jeweils **mit** gültigem Token - erwarte die bekannten Erfolgscodes (`200`/`201`) statt `401`.
6. Teste eine Route mit einem absichtlich falschen Token - erwarte `401`.
7. Committe die Änderungen.

## Checkpoint

- Alle drei getesteten `/tickets`-Routen liefern ohne Token `401` und mit gültigem Token den erwarteten Erfolgscode.

## Abschlusskriterien

- Kein bestehender Routen-Handler aus Modul 14/15 wurde inhaltlich verändert - nur die vorgeschaltete Middleware ist neu.

## Fallback

Falls `jq` zum Auslesen des Tokens aus der Login-Antwort nicht installiert ist: die Antwort manuell im Terminal ablesen und den Token-String direkt kopieren.
