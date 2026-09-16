# Transfer-Übung Modul 19 - Übung: Kompletten TeamBoard-Fluss ohne curl demonstrieren

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - nutzt ausschließlich die bestehende Oberfläche, ändert keinen Code.

## Ziel

Den kompletten TeamBoard-Fluss (Login → Ticket anlegen → Status ändern → Board zeigt Ergebnis) ausschließlich über die React-Oberfläche demonstrieren, ganz ohne `curl` - als Generalprobe für die Live-Demo in Modul 22.

## Ausgangslage

- Backend und Frontend laufen (`docker compose up -d --build` sowie `npm run dev` im `frontend/`-Ordner).

## Aufgaben

1. Registriere (falls noch nicht geschehen) über `curl` einen Testnutzer - dies ist die einzige erlaubte Ausnahme, da es keine Registrierungsoberfläche gibt.
2. Melde dich ausschließlich über das React-Login-Formular an.
3. Lege über das Formular in der Oberfläche zwei neue Tickets an.
4. Bewege eines der beiden Tickets über den "Weiter →"-Button einmal, das andere zweimal.
5. Bestätige visuell, dass sich die Tickets in den korrekten Spalten befinden (eines in "In Progress", eines in "Done").
6. Lade die Browserseite manuell neu (F5) und beobachte, was mit dem Login-Status passiert.

## Checkpoint

- Nach Schritt 4 zeigt das Board ein Ticket in "In Progress" und eines in "Done", ohne dass `curl` für die Statusänderung genutzt wurde.

## Abschlusskriterien

- Der komplette funktionale Fluss lässt sich ausschließlich mit Maus/Tastatur in der Oberfläche zeigen - passend für eine Live-Demo vor Publikum.

## Lösungshinweise

Nach F5 verschwindet der Login-Status, weil der Token nur im React-State (nicht in `localStorage`) gehalten wird (siehe Grenzen in Lab 19.2) - ein erneuter Login über das Formular ist nötig, die zuvor angelegten Tickets bleiben aber in MongoDB erhalten und erscheinen nach dem erneuten Login unverändert.

## Fallback

Falls kein Testnutzer mehr existiert (z. B. nach einem MongoDB-Reset): einmalig erneut per `curl -X POST http://localhost:3000/auth/register ...` registrieren.
