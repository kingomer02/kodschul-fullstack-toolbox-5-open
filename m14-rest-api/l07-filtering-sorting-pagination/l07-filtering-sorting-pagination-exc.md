# Lab 14.7 - Übung: Filtern, Sortieren, Paginieren

**Dauer:** ca. 35 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - `GET /tickets` versteht Query-Parameter.

## Ausgangslage

- Validierung mit zod aus Lab 14.6.

## Aufgaben

1. **Entwirf die Schnittstelle zuerst auf Papier:** Welche Parameter bietet `GET /tickets` an? Mindestens: nach Status filtern, nach Zuständigem filtern, nach einem Feld sortieren (auf- und absteigend), blättern. Wie heißen sie, welche Werte sind erlaubt, welche Obergrenze hat eine Seite?
2. Entscheide, wie der Client die Gesamtzahl der Treffer erfährt - Umschlag-Objekt oder Header - und begründe es mit Blick auf bestehende Clients.
3. Schreib ein zod-Schema für die Query-Parameter.
4. Ergänze in `TicketRepository` eine Methode, die eine geprüfte Anfrage entgegennimmt und die passende Seite **plus** die Gesamtzahl zurückgibt.
5. Stell `GET /tickets` darauf um.
6. Lege zwei, drei zusätzliche Tickets an und teste Kombinationen. Teste auch einen falsch geschriebenen Statuswert, eine Seitengröße aus Buchstaben und einen Tippfehler im Parameternamen.

## Checkpoint

- `?status=To%20Do` liefert nur offene Tickets.
- `?sort=title&order=desc&limit=2&offset=2` liefert die zweite Seite, die Gesamtzahl bleibt die aller Treffer.
- `?status=Todo`, `?limit=abc` und `?stauts=Done` liefern `422`.
- `GET /tickets` ohne Parameter verhält sich wie vorher.

## Abschlusskriterien

- Die Route selbst enthält keine Filter- oder Sortierlogik, nur Prüfen und Weiterreichen.
- Du kannst erklären, warum Paginierung ohne feste Sortierung unzuverlässig ist.

## Fallback

Falls das Leerzeichen in `To Do` Probleme macht: in der URL als `%20` kodieren. `curl` macht das nicht von selbst.

## Zusatz, wenn Zeit bleibt

Beschreibe `GET /tickets` mit allen Parametern als OpenAPI-Ausschnitt (YAML). Kennst du Swagger aus Java, ist das dieselbe Spezifikation.
