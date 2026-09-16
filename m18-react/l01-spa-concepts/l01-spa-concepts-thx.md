# Modul 18: Einstieg in React

## Lab 18.1 - SPA-Grundkonzepte

---

## Lab-Ziel

Du verstehst, was eine Single-Page-Application (SPA) von der bisherigen statischen HTML-Seite (Modul 17) unterscheidet, und kannst eine minimale React-Komponente lesen.

**Leitfragen:**

<details>
<summary>Was ändert sich für den Browser, wenn aus `index.html` (Modul 17) eine React-SPA wird?</summary>

Statt bei jeder Aktion eine neue HTML-Seite vom Server zu laden, rendert JavaScript im Browser die Oberfläche direkt neu - die Seite selbst wird nur einmal geladen ("Single Page").

</details>

<details>
<summary>Was ist eine "Komponente" in React auf einem sehr einfachen Niveau?</summary>

Eine Funktion, die JSX (HTML-ähnlichen Code) zurückgibt und damit einen wiederverwendbaren Teil der Oberfläche beschreibt.

</details>

---

## Minimalbeispiel: Zähler-Komponente

```tsx
// sample-react/src/Counter.tsx
import { useState } from "react";

export function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Aktueller Wert: {count}</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  );
}
```

- `useState(0)` erzeugt einen Zustand (`count`) mit Startwert `0` sowie eine Funktion (`setCount`), um ihn zu ändern.
- Ein Klick auf den Button ändert `count`, React rendert daraufhin automatisch nur den betroffenen Teil der Seite neu - kein manuelles DOM-Update nötig.

---

## Vergleich zu Modul 17

| Aspekt                      | Statisches HTML (Modul 17)  | React-SPA (ab Modul 18)                    |
| --------------------------- | --------------------------- | ------------------------------------------ |
| Inhalt ändert sich durch    | neue Seite vom Server laden | JavaScript-Zustand im Browser (`useState`) |
| Wiederverwendbare Bausteine | keine (nur Kopien im HTML)  | Komponenten (z. B. `<Counter />`)          |

---

## Checkpoint

Ein Klick auf den Button erhöht die angezeigte Zahl, ohne dass die Seite neu lädt - beobachtbar am fehlenden "Neuladen"-Effekt im Browser.

Weiter geht es mit Lab 18.2: Komponenten und State für TeamBoard-Tickets.
