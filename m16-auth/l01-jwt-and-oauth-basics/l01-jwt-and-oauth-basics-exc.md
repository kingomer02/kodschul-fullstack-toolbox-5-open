# Lab 16.1 - Übung: JWT und OAuth: Grundlagen

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - eigenständiges Beispielprojekt.

## Vorbereitung

- Ein leerer Ordner `sample-auth/` mit `npm init -y` und `npm install express jsonwebtoken` sowie `npm install --save-dev typescript @types/express @types/jsonwebtoken @types/node` liegt bereit.

## Aufgaben

1. Erstelle `sample-auth/src/server.ts` mit `POST /login` (liefert einen JWT für einen übergebenen `username`) und einer geschützten Route `GET /profile` mit `requireAuth`-Middleware.
2. Starte den Server und teste `POST /login` mit `curl`.
3. Teste `GET /profile` **ohne** `Authorization`-Header - erwarte `401`.
4. Teste `GET /profile` **mit** dem Token aus Schritt 2 als `Authorization: Bearer <token>` - erwarte `200`.
5. Verändere ein einzelnes Zeichen im Token und wiederhole Schritt 4 - erwarte erneut `401`.

## Checkpoint

- Schritt 3 und 5 liefern beide `401`; Schritt 4 liefert `200`.

## Abschlusskriterien

- Du kannst erklären, warum das Verändern eines einzigen Zeichens im Token in Schritt 5 zu einem Fehler führt (Signaturprüfung schlägt fehl).

## Fallback

Falls `jsonwebtoken`-Typen Konflikte verursachen: `const jwt = require("jsonwebtoken")` als Alternative zum ES-Modul-Import verwenden.
