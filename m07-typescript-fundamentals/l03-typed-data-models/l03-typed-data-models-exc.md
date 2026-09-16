# Lab 7.3 - Übung: Datenmodelle typisieren

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - das `Ticket`-Modell wird erstmals im Code angelegt.

## Ausgangslage

Das Backend-TypeScript-Setup existiert (Modul 6); der `Ticket`-Contract liegt unter `project/contracts/ticket-contract.md`.

## Aufgaben

1. Lege `backend/src/models/ticket.ts` an und definiere dort `interface Ticket` exakt gemäß dem Contract.
2. Lege in derselben Datei zwei Beispielobjekte vom Typ `Ticket` mit unterschiedlichem `status` an.
3. Versuche absichtlich, einem der Beispielobjekte einen ungültigen `status`-Wert (z. B. `"Todo"`) zuzuweisen, und beobachte den Kompilierfehler.
4. Korrigiere den Fehler und exportiere `Ticket` (`export interface Ticket ...`), damit spätere Module es importieren können.

## Checkpoint

- `npm run build` (aus Modul 6) kompiliert `ticket.ts` fehlerfrei.
- `Ticket` ist exportiert und identisch zum Contract in `project/contracts/ticket-contract.md`.

## Abschlusskriterien

- Beide Beispielobjekte haben unterschiedliche, aber jeweils gültige `status`-Werte.

## Fallback

Bei Unsicherheit über String-Union-Syntax: die Contract-Datei direkt als Vorlage kopieren und nur den Dateipfad/Export anpassen.
