# Lab 8.3 - Übung: Einstieg in Generics

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - `TicketRepository` wird auf eine generische Basis umgestellt.

## Ausgangslage

`TicketRepository` mit `private tickets: Ticket[]` existiert (Lab 8.2).

## Aufgaben

1. Schreibe eine generische Klasse `Repository<T extends { id: string }>` mit `add(item: T): void` und `findById(id: string): T | undefined`.
2. Lasse `TicketRepository` von `Repository<Ticket>` erben (`class TicketRepository extends Repository<Ticket> {}`), statt die Logik zu duplizieren.
3. Prüfe, dass `add`/`findById` mit `Ticket`-Objekten weiterhin wie in Lab 8.2 funktionieren.
4. Lege probeweise eine zweite generische Nutzung an, z. B. `Repository<{ id: string; label: string }>`, um zu zeigen, dass die Klasse mit anderen Formen wiederverwendbar ist.
5. Lege `backend/src/services/ticket-service.ts` an mit `class TicketService`, die im Konstruktor ein `private repository: TicketRepository` entgegennimmt, und einer Methode `moveToNextStatus(id: string): Ticket | undefined`, die den Status um genau einen Schritt in der Reihenfolge `"To Do" -> "In Progress" -> "Done"` weiterschaltet (am Ende der Reihenfolge bleibt der Status auf `"Done"`).
6. Instanziiere `TicketService` mit einer `TicketRepository`-Instanz, die bereits ein Ticket enthält, und rufe `moveToNextStatus` zweimal hintereinander mit derselben ID auf.

## Checkpoint

- `TicketRepository` hat keine eigene `tickets`-Liste mehr, sondern nutzt die geerbte generische Logik.
- Das Verhalten für `Ticket` bleibt identisch zu Lab 8.2 (gleiche Test-IDs liefern gleiche Ergebnisse).
- `TicketService.moveToNextStatus` schaltet den Status korrekt weiter und bleibt bei `"Done"` stehen, statt einen Fehler zu werfen oder über das Ende der Reihenfolge hinauszulaufen.

## Abschlusskriterien

- `npm run build` kompiliert fehlerfrei.
- Der zweite generische Anwendungsfall (Aufgabe 4) kompiliert ebenfalls fehlerfrei, ohne Änderung an `Repository<T>` selbst.

## Fallback

Bei Unsicherheit über `extends { id: string }`: zunächst ohne Einschränkung (`class Repository<T>`) arbeiten, den resultierenden Fehler bei `item.id` in `findById` gemeinsam mit dem Trainer nachvollziehen, dann die Einschränkung ergänzen.
