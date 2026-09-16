# Lab 18.1 - Übung: SPA-Grundkonzepte

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - eigenständiges Beispielprojekt.

## Vorbereitung

- Ein neues Vite-React-TS-Projekt liegt bereit: `npm create vite@latest sample-react -- --template react-ts`, danach `npm install` im erzeugten Ordner.

## Aufgaben

1. Erstelle `sample-react/src/Counter.tsx` mit einer `Counter`-Komponente, die einen Zähler per `useState` verwaltet und einen "+1"-Button anzeigt.
2. Binde `<Counter />` in `sample-react/src/App.tsx` ein.
3. Starte den Dev-Server (`npm run dev`) und klicke den Button mehrfach - beobachte, dass die Seite dabei nicht neu lädt.
4. Ergänze einen zweiten Button "Zurücksetzen", der `count` auf `0` setzt.

## Checkpoint

- Der Zähler erhöht sich bei jedem Klick auf "+1" und wird durch "Zurücksetzen" wieder auf `0` gesetzt - beides ohne sichtbares Neuladen der Seite.

## Abschlusskriterien

- Du kannst in eigenen Worten erklären, warum React nach einem Klick nur den Text mit der Zahl neu rendert, statt die komplette Seite neu zu laden.

## Fallback

Falls `npm create vite@latest` wegen Netzwerkproblemen fehlschlägt: ein bereits vom Trainer bereitgestelltes Vite-Starterprojekt verwenden.
