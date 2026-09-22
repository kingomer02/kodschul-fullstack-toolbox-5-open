# Modul 19: React trifft die gesicherte API

## Lab 19.8 - Vertiefung Hooks (5/6): `useReducer`

---

## Lab-Ziel

Bisher lädt das Board nach **jeder** Aktion die komplette Liste neu - zwei Anfragen pro Klick, und alle Karten rendern neu. Die API liefert das geänderte Ticket aber schon zurück. Du führst den Board-Zustand über einen **Reducer**: eine Funktion, die aus altem Zustand und einer Aktion den neuen Zustand berechnet.

**Leitfragen:**

<details>
<summary>Was ist ein Reducer?</summary>

Eine **reine** Funktion `(zustand, aktion) => neuerZustand`. Rein heißt: kein `fetch`, kein `setState`, kein Zufall - gleiche Eingabe, gleiche Ausgabe. Alle möglichen Zustandsänderungen stehen an **einer** Stelle, und jede hat einen Namen (`loaded`, `created`, `updated`, `failed`).

</details>

<details>
<summary>Wann `useReducer` statt `useState`?</summary>

Wenn mehrere Zustandswerte zusammengehören und sich gemeinsam ändern (Liste + Fehlermeldung), oder wenn der neue Zustand vom alten abhängt (ein Ticket in der Liste ersetzen). Für einen einzelnen Wert - ein Suchfeld, eine Checkbox - bleibt `useState` einfacher.

</details>

---

## Aufbau

```tsx
type BoardAction =
  | { type: "loaded"; tickets: Ticket[] }
  | { type: "updated"; ticket: Ticket }
  | ...;

function boardReducer(state: BoardState, action: BoardAction): BoardState {
  switch (action.type) {
    case "loaded":  return { ... };
    case "updated": return { ... };
  }
}

const [board, dispatch] = useReducer(boardReducer, initialBoard);
dispatch({ type: "updated", ticket });   // statt setTickets(...)
```

Der `switch` über `action.type` ist ein **Discriminated Union**: TypeScript weiß in jedem `case`, welche Felder die Aktion hat, und meldet einen Fehler, wenn ein Fall fehlt.

**Unveränderlich ersetzen, nicht ändern:** Der Reducer gibt ein **neues** Array zurück, in dem nur das geänderte Ticket ein neues Objekt ist. Alle anderen Ticket-Objekte bleiben dieselben - und `memo` aus Lab 19.6 kann ihre Karten überspringen.

---

## Brücke zu dem, was du kennst

Das Muster heißt anderswo Event Sourcing oder Zustandsautomat: Ereignisse mit Namen, eine Funktion, die sie anwendet. Der `switch` über einen Discriminated Union entspricht einem `switch` über `sealed`-Klassen in Java 21 mit Pattern Matching - inklusive der Prüfung, dass alle Fälle abgedeckt sind.

---

## Checkpoint

Ein Klick auf "Weiter →" schickt **eine** Anfrage und rendert **eine** Karte neu. Schlägt eine Aktion fehl, steht eine Meldung über dem Board.

## Projektbezug

`api.ts` gibt jetzt die Antwort der API zurück (das angelegte bzw. geänderte Ticket), statt sie wegzuwerfen.
