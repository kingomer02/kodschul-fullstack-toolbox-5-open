# Lab 19.3 - Übung: Vertiefende Übung: Aktionen aus der Oberfläche auslösen

**Dauer:** ca. 45 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - ergänzt echte Schreibaktionen (Ticket anlegen, Status ändern) direkt in der Oberfläche.

## Ausgangslage

- Das Board aus Lab 19.2 zeigt echte, geladene Tickets nach Login.

## Aufgaben

1. Erweitere `TicketCard` um einen Button "Weiter →", der `PATCH /tickets/:id/status` mit dem aktuellen Token aufruft.
2. Erstelle `NewTicketForm` mit einem Eingabefeld und einem Button, der `POST /tickets` aufruft.
3. Ergänze in `App.tsx` eine Funktion `loadTickets(token)`, die die Ticketliste neu vom Server lädt, und rufe sie sowohl beim initialen Login als auch nach jeder erfolgreichen Aktion (`onChanged`, `onCreated`) auf.
4. Reiche `token` und die passenden Callback-Funktionen von `App` über `Column` bis zu `TicketCard` als Props durch.
5. Teste: lege ein neues Ticket über das Formular an und bestätige, dass es sofort in "To Do" erscheint.
6. Teste: klicke "Weiter →" auf einem Ticket und bestätige, dass es in die nächste Spalte wechselt.
7. Committe die Änderungen.

## Checkpoint

- Ein neu angelegtes Ticket erscheint ohne manuelles Neuladen der Seite in "To Do".
- Ein Klick auf "Weiter →" bewegt ein Ticket sichtbar von "To Do" zu "In Progress" (bzw. weiter zu "Done").

## Abschlusskriterien

- Nach jeder Aktion (Anlegen, Status ändern) zeigt das Board konsistent den tatsächlichen Server-Stand, nicht nur eine lokale Vermutung.

## Fallback

Falls das Durchreichen von Props über mehrere Komponentenebenen unübersichtlich wird: zunächst nur `TicketCard` direkt in `App.tsx` ohne `Column`-Zwischenschicht testen, dann schrittweise wieder einbauen.
