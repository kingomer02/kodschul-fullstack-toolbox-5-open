# Lab 19.2 - Übung: Datenfluss: Login, Token und echte Tickets laden

**Dauer:** ca. 60 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - ersetzt hartcodierte Beispieldaten durch echte Login- und Ticketabfragen gegen das Backend.

## Ausgangslage

- Backend läuft containerisiert mit Auth (Modul 16); Frontend zeigt hartcodierte Tickets (Modul 18).

## Aufgaben

1. Installiere `cors` (inkl. Typen) im `backend/`-Ordner und aktiviere `app.use(cors())` in `index.ts`.
2. Baue neu und starte: `docker compose up -d --build`.
3. Erstelle `frontend/src/components/LoginForm.tsx` mit zwei kontrollierten Eingabefeldern (`username`, `password`) und einem `onLoggedIn`-Callback.
4. Baue `App.tsx` so um, dass ohne Token nur `LoginForm` angezeigt wird und nach erfolgreichem Login per `useEffect` echte Tickets von `GET /tickets` (mit `Authorization`-Header) geladen werden.
5. Filtere die geladenen Tickets nach `status` und übergib sie an die passenden `Column`-Komponenten.
6. Registriere (falls noch nicht geschehen) einen Testnutzer über `curl` gegen `/auth/register`, logge dich dann über das React-Formular ein.
7. Bestätige, dass das Board echte, zuvor über `curl` angelegte Tickets anzeigt.

## Checkpoint

- Ohne Login zeigt die Seite ausschließlich das Formular.
- Nach erfolgreichem Login zeigt das Board reale Tickets aus MongoDB, nicht die hartcodierten Beispiele aus Modul 18.

## Abschlusskriterien

- Ein absichtlich falsches Passwort im Formular zeigt eine Fehlermeldung, statt die Seite unbehandelt abstürzen zu lassen.

## Fallback

Falls die Anfrage im Browser mit einem CORS-Fehler in der Konsole fehlschlägt: prüfen, ob `app.use(cors())` **vor** den betroffenen Routen registriert wurde und der Container neu gebaut wurde.
