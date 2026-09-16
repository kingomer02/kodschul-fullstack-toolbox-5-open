# Lab 19.1 - Übung: Eine Komponente an eine öffentliche Test-API anbinden

**Dauer:** ca. 20 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - eigenständiges Beispielprojekt mit einer öffentlichen Test-API.

## Vorbereitung

- Ein neues oder bestehendes Vite-React-TS-Projekt (z. B. `sample-fetch`) liegt bereit.

## Aufgaben

1. Erstelle eine `UserList`-Komponente, die per `useEffect` Nutzer von `https://jsonplaceholder.typicode.com/users` lädt.
2. Ergänze einen `loading`-Zustand, der "Lädt..." anzeigt, bis die Antwort eintrifft.
3. Rendere die geladenen Namen als Liste.
4. Öffne die Entwicklertools (Netzwerk-Tab) und beobachte die tatsächliche Anfrage beim Laden der Seite.

## Checkpoint

- Beim ersten Laden erscheint kurz "Lädt...", danach die vollständige Namensliste.

## Abschlusskriterien

- Du kannst erklären, was passieren würde, wenn der `fetch`-Aufruf versehentlich außerhalb von `useEffect` direkt im Komponentenkörper stünde (Endlosschleife von Netzwerkaufrufen bei jedem Rendern).

## Fallback

Falls `jsonplaceholder.typicode.com` im Schulungsnetzwerk nicht erreichbar ist: eine andere öffentliche Test-API (z. B. `https://api.github.com/users`) mit angepasstem Antwortformat verwenden.
