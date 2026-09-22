# Lab 14.5 - Übung: Router und zentrale Fehlerbehandlung

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - Ticket-Routen wandern in einen Router, Fehler werden zentral behandelt.

## Ausgangslage

- Die API aus Lab 14.4 mit sieben Ticket-Routen in `index.ts`.

## Aufgaben

1. **Erst den Ist-Zustand ansehen.** Schick einen Body mit kaputtem JSON an `POST /tickets` (z. B. ein Komma zu viel) und ruf eine Route auf, die es nicht gibt. Was genau kommt zurück, was steht im Server-Log?
2. Lege eine Fehlerklasse an, die einen HTTP-Status und optionale Details mitträgt.
3. Schreib eine Middleware für unbekannte Routen und eine Fehler-Middleware. Die Fehler-Middleware unterscheidet: eigene Fehler, kaputtes JSON, alles andere.
4. Zieh die Ticket-Routen aus `index.ts` in einen eigenen Router `src/routes/ticket-routes.ts`. Die Routen werfen im Fehlerfall nur noch, statt selbst zu antworten.
5. Häng in `index.ts` alles in der richtigen Reihenfolge ein. Überlege vorher: Was passiert, wenn die Fehler-Middleware **vor** den Routen steht?
6. Beweise den `500`-Fall: Bau vorübergehend eine Route, die einen normalen `Error` wirft, ruf sie auf und vergleiche die Antwort mit dem Server-Log. Danach wieder entfernen.

## Checkpoint

- Kaputtes JSON → `400` mit `{"error": "..."}`, kein HTML.
- Unbekannte Route → `404` mit JSON.
- Unerwarteter Fehler → `500` ohne Details beim Client, Stacktrace im Server-Log.
- Alle Antworten aus Lab 14.4 funktionieren unverändert.

## Abschlusskriterien

- `index.ts` enthält keine einzelne Ticket-Route mehr, nur noch das Einhängen.
- Du kannst erklären, warum die Reihenfolge der `app.use`-Aufrufe entscheidet.

## Fallback

Falls die Fehler-Middleware nie aufgerufen wird: Hat sie wirklich **vier** Parameter? Auch wenn `next` nicht benutzt wird, muss er in der Signatur stehen.
