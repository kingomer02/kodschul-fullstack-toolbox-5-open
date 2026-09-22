# Lab 14.6 - Übung: Eingaben validieren mit zod

**Dauer:** ca. 35 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - alle schreibenden Ticket-Routen prüfen ihre Eingaben mit zod.

## Ausgangslage

- Router und zentrale Fehlerbehandlung aus Lab 14.5.

## Aufgaben

1. **Ist-Zustand prüfen.** Schick an `POST /tickets` einen Titel, der eine Zahl ist, einen Titel aus Leerzeichen und ein zusätzliches Feld `"priority": "hoch"`. Was wird gespeichert?
2. Installiere `zod` im `backend/`-Ordner.
3. Lege `src/validation/ticket-schemas.ts` an mit je einem Schema für: Ticket anlegen, Ticket ändern (`PATCH`), Ticket zuweisen. Überlege für jedes Feld: Pflicht oder optional? Grenzen? Unbekannte Felder erlauben?
4. Schreib eine kleine Hilfsfunktion `validate(schema, data)`, die geprüfte Daten zurückgibt oder einen `HttpError` mit Status `422` und einer Liste der Fehler wirft.
5. Ersetze in den Routen die Handprüfungen (`if (!title) ...`) durch deine Schemas.
6. Wiederhole die Anfragen aus Aufgabe 1 und vergleiche.
7. **Gezielt die Stolperfalle testen:** Schick `PATCH /tickets/t-1` mit **nur** `{"assignee": "..."}` und prüfe danach mit `GET`, ob die Beschreibung noch da ist.

## Checkpoint

- Zahl als Titel, leerer Titel und unbekannte Felder → `422` mit Details pro Feld.
- `"  Tests schreiben  "` wird als `"Tests schreiben"` gespeichert.
- `PATCH` mit nur einem Feld lässt alle anderen Felder unverändert.
- `PATCH` mit `status` wird weiterhin abgelehnt - jetzt durch das Schema.

## Abschlusskriterien

- In den Routen steht keine einzige Handprüfung mehr auf `req.body`.
- Du kannst erklären, warum `z.infer` besser ist, als ein Interface und ein Schema getrennt zu pflegen.

## Fallback

Falls TypeScript meckert, dass `validate` `unknown` zurückgibt: Die Funktion braucht einen generischen Typparameter für das Schema - `z.infer<S>` liefert dann den passenden Rückgabetyp.
