# Transfer-Übung Modul 18 - Übung: Vierte Spalte als eigenständige Komponentenübung

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - fügt testweise eine vierte, nicht im Plan vorgesehene Spalte hinzu, um Komponentenwiederverwendung zu üben, und entfernt sie danach wieder.

## Ziel

Bestätigen, dass `Column` und `TicketCard` echte, wiederverwendbare Komponenten sind, indem eine komplett neue Spalte ohne Codeduplizierung ergänzt wird.

## Ausgangslage

- Das React-Board aus Lab 18.3 läuft mit drei Spalten (To Do, In Progress, Done).

## Aufgaben

1. Ergänze in `sample-tickets.ts` testweise eine vierte Kategorie `blocked: [...]` mit 1-2 Beispieltickets.
2. Ergänze in `App.tsx` eine vierte `<Column title="Blocked" initialTickets={sampleTickets.blocked} />`, ohne `Column` oder `TicketCard` selbst zu verändern.
3. Passe das Grid-Layout testweise an (z. B. `col-md-3` statt `col-md-4`) und prüfe im Browser, dass alle vier Spalten sinnvoll nebeneinander passen.
4. Entferne die vierte Spalte anschließend wieder vollständig (Code und Beispieldaten), da sie nicht Teil des offiziellen TeamBoard-Status-Modells (`To Do`/`In Progress`/`Done`) ist.
5. Bestätige per `git status`, dass der Arbeitsbaum wieder dem Stand aus Lab 18.3 entspricht.

## Checkpoint

- Die vierte Spalte rendert korrekt, solange sie existiert, ausschließlich durch Wiederverwendung von `Column`/`TicketCard`.
- Nach Schritt 4 zeigt `git status` keine verbleibenden Änderungen gegenüber dem letzten Commit.

## Abschlusskriterien

- Kein Code in `Column.tsx` oder `TicketCard.tsx` musste für die zusätzliche Spalte verändert werden.

## Lösungshinweise

```tsx
<Column title="Blocked" initialTickets={sampleTickets.blocked} />
```

```bash
git checkout -- .
git status
# nothing to commit, working tree clean
```

## Fallback

Falls `git checkout -- .` nicht alle Teständerungen zurücksetzt (z. B. neu erstellte Dateien): betroffene Dateien manuell löschen und mit `git status` erneut prüfen.
