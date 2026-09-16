# Lab 15.2 - Lösung: SQL versus NoSQL: Ticket-Daten modellieren

## Aufgabe 1: SQL-Modell

```sql
CREATE TABLE tickets (
  id UUID PRIMARY KEY,
  title VARCHAR(255) NOT NULL,
  description TEXT,
  assignee VARCHAR(255),
  status VARCHAR(20) NOT NULL DEFAULT 'To Do'
);

CREATE TABLE comments (
  id UUID PRIMARY KEY,
  ticket_id UUID NOT NULL REFERENCES tickets(id),
  author VARCHAR(255) NOT NULL,
  text TEXT NOT NULL
);
```

## Aufgabe 2: MongoDB-Modell

```json
{
  "_id": "t-1",
  "title": "Login-Formular bauen",
  "description": "E-Mail und Passwort-Feld",
  "assignee": "Alex",
  "status": "To Do",
  "comments": [
    { "author": "Sam", "text": "Bitte auch Validierung ergänzen." },
    { "author": "Alex", "text": "Erledigt." }
  ]
}
```

## Aufgabe 3: Empfehlung

Für TeamBoard passt das MongoDB-Modell mit eingebetteten Kommentaren besser: Kommentare werden praktisch immer zusammen mit ihrem Ticket gelesen, wodurch ein einziger Lesezugriff (statt eines JOINs über zwei Tabellen) ausreicht.

## Aufgabe 4: Diskussion - viele Kommentare

Bei sehr vielen Kommentaren wächst das Dokument stetig und wird bei jedem Lesezugriff komplett mitgeladen - ab einer gewissen Größe wäre eine separate `comments`-Collection mit Referenz auf die Ticket-ID die bessere Wahl.

## Grenzen

Diese Übung ist bewusst vereinfacht; reale Entscheidungen hängen zusätzlich von Zugriffsmustern, Skalierung und Team-Erfahrung ab.
