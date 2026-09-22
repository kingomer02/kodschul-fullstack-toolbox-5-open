# Modul 19: React trifft die gesicherte API

## Lab 19.4 - Vertiefung Hooks (1/6): Wann rendert React?

---

## Lab-Ziel

Alle Hooks, die heute folgen (`useMemo`, `useCallback`, `useRef`, `useReducer`, Context), beantworten dieselbe Frage: **Was passiert, wenn React eine Komponente neu rendert?** Bevor du einen davon einsetzt, misst du deshalb, wann welche Komponente rendert.

**Leitfragen:**

<details>
<summary>Was heißt "rendern" in React überhaupt?</summary>

React ruft die Komponenten-**Funktion** erneut auf. Sie liefert eine neue Beschreibung der Oberfläche (JSX), React vergleicht sie mit der vorherigen und ändert im Browser nur, was sich unterscheidet. Rendern ist also nicht "DOM neu bauen", sondern "Funktion neu ausführen".

</details>

<details>
<summary>Wodurch rendert eine Komponente neu?</summary>

Drei Auslöser:
1. Ihr **eigener State** ändert sich (Setzfunktion von `useState`).
2. Ihre **Eltern-Komponente** rendert neu - dann rendern standardmäßig **alle** Kinder mit, egal ob sich ihre Props geändert haben.
3. Ein **Context**, den sie liest, ändert sich (Lab 19.9).

Props allein lösen nichts aus - sie ändern sich nur, **weil** die Eltern-Komponente neu rendert.

</details>

---

## Die drei Regeln, die alles Weitere erklären

**1 · State ist eine Momentaufnahme.** Innerhalb eines Renderings ist `count` eine ganz normale Konstante. `setCount(5)` ändert sie nicht, sondern bestellt ein neues Rendering, in dem `count` dann 5 ist.

**2 · Der Anfangswert von `useState` zählt nur einmal.** `useState(initialTickets)` liest `initialTickets` beim **ersten** Rendern. Kommen später andere Props herein, ignoriert React sie. Deshalb gilt:

> **Was sich aus Props oder anderem State berechnen lässt, ist kein State.**

**3 · StrictMode rendert im Entwicklungsmodus doppelt.** `<StrictMode>` in `main.tsx` ruft jede Komponente absichtlich zweimal auf, um unsaubere Seiteneffekte aufzudecken. Im fertigen Build (`npm run build`) passiert das nicht. Zählst du Renderings, zählst du im Entwicklungsmodus also alles doppelt.

---

## Brücke zu dem, was du kennst

In Swing/JavaFX änderst du ein Widget direkt (`label.setText(...)`). In React beschreibst du, **was** bei einem Zustand zu sehen sein soll, und React rechnet den Unterschied aus. Näher dran ist ein Server-Template (Thymeleaf, Jinja): Daten rein, HTML raus - nur dass React das bei jeder Zustandsänderung im Browser wiederholt.

---

## Checkpoint

Du kannst vorhersagen, welche Komponenten bei einem Tastendruck im Formular und bei einem Klick auf "Weiter →" neu rendern - und die Zahlen stimmen mit deiner Messung überein.

## Projektbezug

Die Messung zeigt: Ein Klick rendert das ganze Board neu. Bei drei Tickets egal - in Lab 19.5 und 19.6 wird es das nicht mehr sein.
