# Lab 14.4 - Übung: Ressourcen schneiden und HTTP-Methoden richtig einsetzen

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - die Ticket-API bekommt `PATCH /tickets/:id` und `DELETE /tickets/:id`.

## Ausgangslage

- Die Express-API aus Lab 14.2/14.3 mit den fünf Routen läuft.

## Aufgaben

1. **Erst entscheiden, dann bauen.** Schreib dir in zwei, drei Stichpunkten auf: Welche Felder soll ein generisches `PATCH /tickets/:id` ändern dürfen - und welches bewusst nicht? Begründe.
2. Ergänze im generischen `Repository<T>` die Methoden, die du dafür brauchst (Ändern und Löschen). Die Signaturen legst du selbst fest.
3. Baue `PATCH /tickets/:id` nach deiner Entscheidung aus Aufgabe 1. Nur die mitgeschickten Felder ändern sich, alle anderen bleiben.
4. Baue `DELETE /tickets/:id`. Überlege, welcher Statuscode bei Erfolg passt und was ein zweiter Aufruf liefern soll.
5. Sorge dafür, dass `POST /tickets` der Aufruferin sagt, wo das neue Ticket liegt.
6. Teste alles mit `curl -i` (das `-i` zeigt Statuscode und Header). Teste auch: Was passiert bei `PUT /tickets/t-1`?

## Checkpoint

- `PATCH /tickets/t-1` mit `{"assignee": "..."}` ändert nur den Zuständigen, Titel und Beschreibung bleiben.
- `PATCH /tickets/t-1` mit `{"status": "Done"}` wird abgelehnt.
- `DELETE` liefert beim ersten Mal `204`, beim zweiten Mal `404`.
- `POST /tickets` liefert einen `Location`-Header.

## Abschlusskriterien

- Du kannst erklären, warum `DELETE` idempotent ist, obwohl die zweite Antwort anders aussieht als die erste.
- Du kannst begründen, warum der Statuswechsel eine eigene Aktion bleibt.

## Fallback

Falls `PATCH` Felder überschreibt, die gar nicht mitgeschickt wurden: prüfen, ob `undefined`-Werte aus dem Body mit in das Update wandern.
