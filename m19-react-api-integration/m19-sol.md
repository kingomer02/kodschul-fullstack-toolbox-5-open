# Transfer-Übung Modul 19 - Lösung: Kompletten TeamBoard-Fluss ohne curl demonstrieren

## Aufgabe 1: Testnutzer (einmalige Ausnahme)

```bash
curl -X POST http://localhost:3000/auth/register \
  -H "Content-Type: application/json" -d '{"username": "demo", "password": "demo1234"}'
```

## Aufgabe 2: Login über die Oberfläche

Im Browser: `demo`/`demo1234` im Login-Formular eingeben und absenden - das Board erscheint.

## Aufgabe 3: Zwei Tickets anlegen

Über `NewTicketForm`: "Demo-Ticket A" und "Demo-Ticket B" nacheinander eingeben und anlegen - beide erscheinen in "To Do".

## Aufgabe 4: Status bewegen

- "Demo-Ticket A": einmal "Weiter →" klicken → wechselt nach "In Progress".
- "Demo-Ticket B": zweimal "Weiter →" klicken → wechselt über "In Progress" nach "Done".

## Aufgabe 5: Visuelle Bestätigung

Das Board zeigt "Demo-Ticket A" in der mittleren Spalte und "Demo-Ticket B" in der rechten Spalte - beide sichtbar ohne jede `curl`-Anfrage bewegt.

## Aufgabe 6: Verhalten nach F5

Nach einem manuellen Neuladen (F5) zeigt die Seite wieder das Login-Formular, da der Token nur im React-State lag. Nach erneutem Login mit `demo`/`demo1234` erscheinen beide Tickets weiterhin korrekt in "In Progress" bzw. "Done" - der MongoDB-Stand blieb unverändert.

## Grenzen

Dieser Ablauf demonstriert nur den "glücklichen Pfad" - Fehlerfälle (falsches Passwort, abgelaufener Token) wurden bereits in Modul 16 separat geprüft.
