# Lab 16.2 - Übung: Login-Flow für TeamBoard implementieren

**Dauer:** ca. 40 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - ergänzt Registrierung, Login und eine Auth-Middleware im Backend.

## Ausgangslage

- Backend mit REST/GraphQL-API und MongoDB-Anbindung (Modul 15) läuft.

## Aufgaben

1. Installiere `bcrypt` und `jsonwebtoken` (inkl. Typen) im `backend/`-Ordner.
2. Erstelle `backend/src/auth/users.ts` mit einem `User`-Interface (`username`, `passwordHash`) und einem In-Memory-Array.
3. Erstelle `backend/src/auth/auth-routes.ts` mit `POST /register` (Passwort per `bcrypt` hashen) und `POST /login` (Passwort prüfen, JWT ausstellen).
4. Binde die Auth-Routen unter dem Präfix `/auth` in `index.ts` ein.
5. Erstelle `backend/src/auth/require-auth.ts` mit einer `requireAuth`-Middleware (noch ohne sie einzusetzen - das folgt in Lab 16.3).
6. Ergänze `JWT_SECRET` als Umgebungsvariable in `docker-compose.yml` beim `backend`-Service.
7. Teste `POST /auth/register` und `POST /auth/login` mit `curl`; teste zusätzlich ein Login mit falschem Passwort (`401`).

## Checkpoint

- `POST /auth/register` liefert `201` mit dem Nutzernamen.
- `POST /auth/login` mit korrekten Zugangsdaten liefert einen Token; mit falschem Passwort `401`.

## Abschlusskriterien

- Passwörter liegen ausschließlich als `bcrypt`-Hash im Speicher, nie im Klartext.

## Fallback

Falls `bcrypt` (native Bindings) im Container Build-Probleme verursacht: `bcryptjs` (reine JS-Implementierung) als Ersatz mit identischer API verwenden.
