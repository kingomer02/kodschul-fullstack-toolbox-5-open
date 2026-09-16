# Transfer-Übung Modul 6 - Lösung: Vollständiger Umstieg auf TypeScript

## Aufgabe 1-2: Aufräumen und lokal testen

```bash
rm -f backend/src/index.js
cd backend
npm run build
npm start
```

## Aufgabe 3: Push und CI prüfen

```bash
git add -A
git commit -m "chore: complete migration to TypeScript backend"
git push
```

Im Actions-Log auf GitHub prüfen, dass der `build`-Schritt tatsächlich `tsc` ausführt.

## Aufgabe 4: Was fehlt noch für einen echten Server

Beispielantwort: Ein echter HTTP-Server mit Express (`app.listen(...)`) sowie Routen, die auf `TicketRepository`/`TicketService` zugreifen - das folgt in Modul 14.

## Grenzen

`npm run build` muss lokal fehlerfrei laufen, bevor gepusht wird - sonst wird die CI unnötig rot.
