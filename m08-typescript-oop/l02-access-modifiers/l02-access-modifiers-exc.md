# Lab 8.2 - Übung: Access Modifiers

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - `TicketRepository` wird angelegt.

## Ausgangslage

`Ticket`-Interface unter `backend/src/models/ticket.ts` existiert (Lab 7.3).

## Aufgaben

1. Lege `backend/src/repositories/ticket-repository.ts` an mit `class TicketRepository`, einer `private` Liste `tickets: Ticket[]` sowie den Methoden `add(ticket: Ticket): void` und `findById(id: string): Ticket | undefined`.
2. Instanziiere `TicketRepository`, füge zwei Tickets hinzu (aus Lab 7.3 wiederverwenden) und rufe `findById` mit einer gültigen und einer ungültigen ID auf.
3. Versuche absichtlich, `repo.tickets` von außerhalb der Klasse zu lesen, und beobachte den Kompilierfehler.
4. Entferne den fehlerhaften Zugriff wieder, sodass die Datei fehlerfrei kompiliert.

## Checkpoint

- `findById` liefert für die gültige ID das passende Ticket, für die ungültige `undefined`.
- Der direkte Zugriff auf `tickets` von außen wurde als Compilerfehler bestätigt und danach entfernt.

## Abschlusskriterien

- `npm run build` kompiliert das Backend fehlerfrei.

## Fallback

Bei Unsicherheit, was "von außerhalb der Klasse" bedeutet: den Zugriffsversuch in einer separaten Datei/Funktion außerhalb der Klassendefinition schreiben, nicht innerhalb einer Methode.
