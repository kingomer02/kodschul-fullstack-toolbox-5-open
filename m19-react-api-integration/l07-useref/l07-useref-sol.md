# Lab 19.7 - Lösung: `useRef` und Aufräumen in `useEffect`

## Aufgabe 1-2: `App.tsx` (Ausschnitt)

```tsx
import { useCallback, useEffect, useMemo, useRef, useState } from "react";

const searchRef = useRef<HTMLInputElement>(null); // Griff auf das echte DOM-Element

// Taste "/" springt ins Suchfeld - wie bei GitHub
useEffect(() => {
  function onKeyDown(event: KeyboardEvent) {
    const typing = event.target instanceof HTMLInputElement;
    if (event.key === "/" && !typing) {
      event.preventDefault(); // sonst landet das "/" im Feld
      searchRef.current?.focus();
    }
  }
  window.addEventListener("keydown", onKeyDown);
  return () => window.removeEventListener("keydown", onKeyDown); // Aufräumen!
}, []);

// im JSX:
<input ref={searchRef} className="form-control" placeholder="Suchen  ( / )" ... />
```

`[]` als Abhängigkeit: Der Listener wird einmal angemeldet. Er braucht keine Werte aus dem Rendern, nur die Ref - und die bleibt immer dasselbe Objekt.

## Gemessen (09/2026)

```text
vorher fokussiert: BODY
nach Taste '/':    INPUT [Suchen  ( / )] | Wert im Feld: ""
```

## Aufgabe 3: Ohne Aufräumen (Entwicklungsmodus)

```text
Handler-Aufrufe pro Tastendruck OHNE Aufräumen (dev): 2
```

StrictMode führt den Effekt aus, räumt auf und führt ihn erneut aus. Ohne Aufräumfunktion bleibt der erste Listener hängen - jetzt sind es zwei. In der fertigen Anwendung passiert dasselbe, sobald eine Komponente mit so einem Effekt aus- und wieder eingeblendet wird - etwa eine Suchleiste, die nur nach dem Login sichtbar ist: bei jedem Einblenden ein Listener mehr.

## Aufgabe 4: Render-Zähler als State

```text
Error: Too many re-renders. React limits the number of renders to prevent an infinite loop.
Seite leer? true
```

`setRenders` im Rendern bestellt ein neues Rendering, das wieder `setRenders` aufruft - endlos. React bricht ab, die Seite bleibt weiß.

Mit `useRef` geht es, weil eine Änderung **kein** Rendering auslöst:

```tsx
const renders = useRef(0);
renders.current++;   // zählt mit, stößt aber nichts an
```

## Drei Dinge, die aufgeräumt werden müssen

Event-Listener (`removeEventListener`), Timer (`clearTimeout`/`clearInterval`), offene Verbindungen (WebSocket `close()`, laufende `fetch` per `AbortController`).

## Commit

```bash
git add -A
git commit -m "feat: Taste / fokussiert die Suche per useRef"
```

## Grenzen

Eine Ref direkt im Rendern zu **lesen**, um etwas anzuzeigen, ist unzuverlässig: Die Anzeige aktualisiert sich nur, wenn aus einem anderen Grund neu gerendert wird. Refs sind für alles, was man **nicht** sieht.
