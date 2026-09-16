# Modul 7: TypeScript-Grundlagen

## Lab 7.3 - Datenmodelle typisieren

---

## Lab-Ziel

Du hast das `Ticket`-Datenmodell aus dem Projekt-Contract als TypeScript-Interface im TeamBoard-Backend umgesetzt.

**Leitfragen:**

<details>
<summary>Warum wird der `Ticket`-Contract jetzt festgelegt, obwohl REST/GraphQL erst in Modul 14-15 folgen?</summary>

Ein früh festgelegtes, stabiles Datenmodell verhindert, dass spätere Module (API, Auth, Frontend) mit unterschiedlichen Annahmen über die Ticket-Form arbeiten.

</details>

<details>
<summary>Warum ist `status` eine String-Union (`"To Do" | "In Progress" | "Done"`) statt einfach `string`?</summary>

Eine Union erlaubt nur genau diese drei Werte - der Compiler lehnt Tippfehler wie `"Todo"` oder beliebige andere Strings ab, während `string` alles zulassen würde.

</details>

<details>
<summary>Wie unterscheidet sich das hier definierte Interface vom Contract in `project/contracts/ticket-contract.md`?</summary>

Es sollte identisch sein - der Contract ist die verbindliche Referenz, das Interface im Code ist deren TypeScript-Umsetzung.

</details>

---

## Der `Ticket`-Contract

Aus [`project/contracts/ticket-contract.md`](../../project/contracts/ticket-contract.md):

```ts
interface Ticket {
  id: string;
  title: string;
  description: string;
  assignee: string;
  status: "To Do" | "In Progress" | "Done";
}
```

- `status` ist eine String-Literal-Union, kein freier `string` - das begrenzt gültige Werte auf genau drei.

---

## Ein Beispielobjekt typisieren

```ts
const sampleTicket: Ticket = {
  id: "t-1",
  title: "Setup Repo",
  description: "Initial repo structure and README",
  assignee: "Alex",
  status: "To Do",
};
```

**Grenze:** `status: "todo"` (Kleinschreibung) wäre bereits ein Kompilierfehler - die Union ist case-sensitiv exakt wie im Contract definiert.

---

## Checkpoint

`Ticket` ist im Backend als Interface definiert und stimmt exakt mit dem Contract überein; ein Beispielticket kompiliert fehlerfrei.

Weiter geht es mit Modul 8: Objektorientierung in TypeScript.
