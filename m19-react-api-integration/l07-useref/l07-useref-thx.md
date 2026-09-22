# Modul 19: React trifft die gesicherte API

## Lab 19.7 - Vertiefung Hooks (4/6): `useRef` und Aufräumen in `useEffect`

---

## Lab-Ziel

Manches muss eine Komponente sich merken, **ohne** dass eine Änderung ein neues Rendering auslöst: einen Griff auf ein DOM-Element, eine Timer-ID, einen Zähler. Dafür gibt es `useRef`. Nebenbei lernst du, warum ein `useEffect` hinter sich aufräumen muss.

**Leitfragen:**

<details>
<summary>Was ist der Unterschied zwischen `useRef` und `useState`?</summary>

| | `useState` | `useRef` |
|---|---|---|
| überlebt Renderings | ja | ja |
| Änderung löst Rendering aus | **ja** | **nein** |
| ändern | über die Setzfunktion | direkt: `ref.current = ...` |
| gedacht für | alles, was **angezeigt** wird | alles, was **nicht** angezeigt wird |

</details>

<details>
<summary>Warum braucht ein Effekt eine Aufräumfunktion?</summary>

Ein Effekt, der etwas **anmeldet** (Event-Listener, Timer, WebSocket), muss es auch wieder **abmelden**, wenn die Komponente verschwindet oder der Effekt neu läuft. Sonst sammeln sich Listener an. StrictMode macht das im Entwicklungsmodus absichtlich sichtbar: Er führt jeden Effekt einmal aus, räumt auf und führt ihn erneut aus.

</details>

---

## Zwei typische Einsätze

```tsx
// 1 · Griff auf ein DOM-Element
const inputRef = useRef<HTMLInputElement>(null);
<input ref={inputRef} />
inputRef.current?.focus();

// 2 · Wert merken, ohne neu zu rendern
const timerId = useRef<number | null>(null);
timerId.current = window.setTimeout(...);
```

```tsx
useEffect(() => {
  window.addEventListener("keydown", handler);
  return () => window.removeEventListener("keydown", handler);   // Aufräumen
}, []);
```

---

## Brücke zu dem, was du kennst

`useRef` ist ein normales Feld in einer Klasse, das nicht Teil des beobachteten Zustands ist - wie ein `transient`-Feld neben den Properties, die ein UI-Binding auslösen. Die Aufräumfunktion entspricht `removeListener` in Swing oder `close()` in einem `try-with-resources`.

---

## Checkpoint

Die Taste `/` springt ins Suchfeld. Im Entwicklungsmodus läuft der Handler pro Tastendruck genau einmal.

## Projektbezug

Die Tastenkürzel-Logik bleibt im Board. In Lab 19.9 wird `App` schlanker - der Effekt bleibt, wo er ist.
