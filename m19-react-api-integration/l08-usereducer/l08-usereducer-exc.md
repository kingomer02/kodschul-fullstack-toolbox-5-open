# Lab 19.8 - Übung: `useReducer`

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - der Board-Zustand wird per Reducer geführt, Aktionen laden die Liste nicht mehr neu.

## Ausgangslage

- Board mit `memo` und `useCallback` aus Lab 19.6.

## Aufgaben

1. **Ist-Zustand messen.** Wie viele Anfragen an `/tickets` schickt ein Klick auf "Weiter →"? (Netzwerk-Tab.) Wie viele Karten rendern dabei neu?
2. Schau dir an, was `PATCH /tickets/:id/status` und `POST /tickets` **zurückliefern**. Ändere die Funktionen in `api.ts` so, dass sie diese Antwort zurückgeben und bei einem Fehlerstatus eine Exception werfen.
3. Entwirf in `src/board-reducer.ts`: den Zustand (Tickets und eine Fehlermeldung), die möglichen Aktionen als Union-Typ und den Reducer.
4. Stelle `App` auf `useReducer` um. "Weiter →" und "Anlegen" nutzen die Antwort der API statt die Liste neu zu laden. Fehler landen als Aktion im Reducer und werden über dem Board angezeigt.
5. Miss erneut: Anfragen und neu gerenderte Karten pro Klick.
6. **Fehlerfall prüfen:** Lade mit `?demo=3` und klicke "Weiter →" auf einem Demo-Ticket. Den gibt es auf dem Server nicht - was passiert?

## Checkpoint

- Ein Klick auf "Weiter →": eine Anfrage, eine neu gerenderte Karte.
- Ein Klick auf ein Demo-Ticket: Fehlermeldung über dem Board, kein Absturz.

## Abschlusskriterien

- Der Reducer enthält keinen `fetch` und kein `setState`.
- Du kannst erklären, warum jetzt nur noch eine Karte neu rendert.

## Fallback

Falls TypeScript im `switch` meckert, dass die Funktion nicht immer etwas zurückgibt: Hast du für jede Aktion einen `case`? Genau diesen Fehler soll der Union-Typ finden.
