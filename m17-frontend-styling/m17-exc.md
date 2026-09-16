# Transfer-Übung Modul 17 - Übung: Vollständiges statisches Kanban-Board zusammenführen

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - führt Emmet, Grid/Flexbox-Verständnis, Bootstrap, Sass und Gulp zu einem vollständigen statischen Ergebnis zusammen.

## Ziel

Das gesamte Modul 17 in einem Ergebnis bündeln: ein vollständiges, responsives, gestyltes Kanban-Board als statisches HTML - bereit, um in Modul 18/19 durch echte React-Komponenten und Live-Daten ersetzt zu werden.

## Ausgangslage

- `frontend/index.html`, `frontend/styles/main.scss`, `frontend/gulpfile.js` aus Lab 17.3-17.5 liegen vor.

## Aufgaben

1. Nutze Emmet, um in jeder der drei Spalten mindestens ein zusätzliches Beispiel-Ticket als Bootstrap-`card` zu ergänzen.
2. Prüfe im responsiven Modus der Entwicklertools drei Breiten: eine schmale (z. B. 375px), eine mittlere (z. B. 800px) und eine breite (z. B. 1200px) - notiere für jede, wie viele Spalten nebeneinanderstehen.
3. Führe `npx gulp build` erneut aus, um sicherzustellen, dass `main.css` den aktuellen Stand von `main.scss` widerspiegelt.
4. Mache einen Screenshot (oder eine kurze Beschreibung) des fertigen Boards bei mittlerer Breite als Referenz für Modul 18.
5. Committe den finalen Stand.

## Checkpoint

- Bei 375px steht eine Spalte, bei 800px und 1200px stehen drei Spalten nebeneinander (Bootstraps `md`-Breakpoint liegt bei 768px).
- `main.css` spiegelt den aktuellen `main.scss`-Stand wider (kein veralteter Build).

## Abschlusskriterien

- Das statische Board zeigt alle drei Spalten mit Farbcodierung, mindestens einer Ticket-Karte je Spalte, und reagiert sichtbar auf die Fensterbreite.

## Lösungshinweise

```bash
npx gulp build
```

Erwartete Spaltenanzahl: 375px → 1 Spalte, 800px → 3 Spalten, 1200px → 3 Spalten (Bootstraps `col-md-4` ändert sich ab 768px nicht mehr weiter).

## Fallback

Falls die Entwicklertools keine exakten Pixelwerte anzeigen: das Browserfenster manuell in der Breite ziehen und den sichtbaren Umbruchpunkt beobachten.
