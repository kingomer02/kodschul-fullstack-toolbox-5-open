# Modul 19: React trifft die gesicherte API

## Lab 19.6 - Vertiefung Hooks (3/6): `React.memo` und `useCallback`

---

## Lab-Ziel

Lab 19.4 hat gezeigt: Rendert `App`, rendern alle Karten mit. `React.memo` lässt eine Komponente aus, wenn sich ihre Props nicht geändert haben. Du wirst sehen, dass `memo` allein oft **gar nichts** bringt - und warum `useCallback` der fehlende Teil ist.

**Leitfragen:**

<details>
<summary>Wie entscheidet `memo`, ob sich Props geändert haben?</summary>

Es vergleicht jede Prop mit `Object.is` - bei Objekten, Arrays und Funktionen also die **Referenz**, nicht den Inhalt. Zwei Objekte mit gleichem Inhalt sind für `memo` verschieden.

</details>

<details>
<summary>Warum ist eine Funktion bei jedem Rendern "neu"?</summary>

```tsx
function App() {
  async function handleAdvance(id: string) { ... }   // bei JEDEM Aufruf von App ein neues Funktionsobjekt
  return <TicketCard onAdvance={handleAdvance} />;
}
```

Die Funktion wird bei jedem Rendern von `App` neu erzeugt. Für `memo` ist das jedes Mal eine andere Prop - die Karte rendert trotzdem.

</details>

---

## Die drei Werkzeuge im Zusammenspiel

```tsx
// 1 · memo: Komponente nur neu rendern, wenn sich eine Prop ändert
export const TicketCard = memo(function TicketCard({ ticket, onAdvance }: Props) { ... });

// 2 · useCallback: dieselbe Funktion über Renderings hinweg
const handleAdvance = useCallback(async (id: string) => { ... }, [token]);

// 3 · useMemo (Lab 19.5): dasselbe Array/Objekt über Renderings hinweg
const columns = useMemo(() => ..., [tickets, search]);
```

`useCallback(fn, deps)` ist dasselbe wie `useMemo(() => fn, deps)` - nur für Funktionen.

**Wichtig:** `useCallback` und `useMemo` für stabile Referenzen lohnen sich **nur**, wenn der Empfänger mit `memo` geschützt ist (oder den Wert als Abhängigkeit in einem Effekt nutzt). Ohne `memo` beim Kind ist `useCallback` wirkungslos.

---

## Brücke zu dem, was du kennst

`memo` ist wie ein `equals`-Check vor dem Neuzeichnen - nur dass er `==` (Referenzgleichheit) statt `.equals()` verwendet. Wer in Java je `equals` vergessen hat und sich über ein `HashSet` mit Duplikaten gewundert hat, kennt das Problem.

---

## Checkpoint

Du kannst mit Zahlen zeigen, wie viele Karten beim Umschalten von "Zähler" neu rendern: ohne `memo`, mit `memo` allein, mit `memo` und `useCallback`.

## Projektbezug

In Lab 19.8 kommt hinzu: Nach einem Klick auf "Weiter →" bleiben alle anderen Ticket-Objekte **dieselben** - dann rendert nur noch die eine geänderte Karte.
