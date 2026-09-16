# Lab 18.1 - Lösung: SPA-Grundkonzepte

## Aufgabe 1: `Counter.tsx`

```tsx
// sample-react/src/Counter.tsx
import { useState } from "react";

export function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Aktueller Wert: {count}</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
      <button onClick={() => setCount(0)}>Zurücksetzen</button>
    </div>
  );
}
```

## Aufgabe 2: Einbinden

```tsx
// sample-react/src/App.tsx
import { Counter } from "./Counter";

function App() {
  return <Counter />;
}

export default App;
```

## Aufgabe 3-4: Testen

```bash
npm run dev
```

Mehrfaches Klicken auf "+1" erhöht den angezeigten Wert; "Zurücksetzen" setzt ihn auf `0` - die Browser-Adresszeile und der restliche Seiteninhalt bleiben dabei unverändert.

## Grenzen

Der Zustand `count` existiert nur im Arbeitsspeicher des Browser-Tabs - ein Neuladen der Seite (F5) setzt ihn zurück auf `0`.
