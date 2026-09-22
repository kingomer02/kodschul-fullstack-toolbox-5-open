# Lab 19.6 - Übung: `React.memo` und `useCallback`

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - `TicketCard` wird mit `memo` geschützt, die Aktion mit `useCallback` stabilisiert.

## Ausgangslage

- Board mit Suche, Zähler-Schalter und `useMemo` aus Lab 19.5.

## Aufgaben

1. Setz in `TicketCard` eine Log-Zeile, die bei jedem Rendern ausgegeben wird. Lade im Production-Build mit `?demo=20000`.
2. **Vorhersage:** Wie viele Karten rendern, wenn du "Zähler" umschaltest? Die Zähler stehen in `Column`, nicht in der Karte. Dann messen.
3. Schütze `TicketCard` mit `memo`. Vorhersage, dann messen. Überrascht?
4. Finde heraus, **welche** Prop sich bei jedem Rendern ändert. Tipp: Die Karten in "Done" verhalten sich anders als die in den anderen Spalten - warum?
5. Behebe es mit `useCallback`. Welche Abhängigkeiten braucht die Funktion?
6. Miss noch einmal: Umschalten und Tippen in die Suche.
7. Entferne die Log-Zeile.

## Checkpoint

- Ohne `memo`: alle sichtbaren Karten rendern neu.
- Mit `memo`, ohne `useCallback`: nur die Karten in "Done" werden übersprungen.
- Mit beidem: beim Umschalten rendert keine einzige Karte.

## Abschlusskriterien

- Du kannst erklären, warum `memo` ohne `useCallback` hier fast nichts bringt.
- Du kannst sagen, wann `useCallback` **überflüssig** ist.

## Fallback

Falls die Karten trotz `memo` und `useCallback` alle neu rendern: Kommen die Ticket-Objekte bei jedem Rendern neu zustande? Die Demo-Tickets müssen **außerhalb** der Komponente erzeugt werden, nicht in `useMemo`.
