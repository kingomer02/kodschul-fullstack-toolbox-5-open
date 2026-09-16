# Lab 15.2 - Übung: SQL versus NoSQL: Ticket-Daten modellieren

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - konzeptionelle Übung ohne Code-Änderung.

## Aufgaben

1. Entwirf für ein `Ticket` mit einer zusätzlichen Liste von Kommentaren (`comments: [{ author, text }]`) ein SQL-Tabellenmodell (mind. zwei Tabellen: `tickets` und `comments` mit Fremdschlüssel).
2. Entwirf dasselbe Datenmodell als ein einzelnes MongoDB-Dokument mit eingebetteten Kommentaren.
3. Notiere in 3-4 Sätzen, welches der beiden Modelle du für TeamBoards Kommentarfunktion empfehlen würdest und warum.
4. Diskutiere kurz (schriftlich oder mit einem Sitznachbarn): Was passiert im MongoDB-Modell, wenn ein Ticket sehr viele Kommentare bekommt?

## Checkpoint

- Beide Modelle (SQL-Tabellen, MongoDB-Dokument) sind vollständig notiert und enthalten dieselben Informationen (Ticket-Felder + Kommentare).

## Abschlusskriterien

- Deine Empfehlung aus Aufgabe 3 nennt mindestens ein konkretes Kriterium (z. B. Konsistenz, Lesegeschwindigkeit, Flexibilität) statt einer reinen Präferenz.

## Fallback

Falls SQL-Syntax unsicher ist: eine einfache Tabellenskizze in Textform (Spaltennamen + Typen) reicht für diese konzeptionelle Übung aus.
