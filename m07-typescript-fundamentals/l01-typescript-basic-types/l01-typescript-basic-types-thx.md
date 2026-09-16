# Modul 7: TypeScript-Grundlagen

## Lab 7.1 - Basistypen und Type Inference

---

## Lab-Ziel

Du kennst die wichtigsten Basistypen in TypeScript und verstehst, wann der Compiler Typen selbst ableitet (Type Inference).

**Leitfragen:**

<details>
<summary>Welche Basistypen gibt es in TypeScript?</summary>

U. a. `string`, `number`, `boolean`, `null`, `undefined`, Arrays (`string[]`), Tupel und `any`/`unknown` als Sonderfälle.

</details>

<details>
<summary>Was ist Type Inference, und wann sollte man trotzdem explizit typisieren?</summary>

Der Compiler leitet aus dem zugewiesenen Wert automatisch den Typ ab (`let x = 5` → `number`); explizite Typen lohnen sich vor allem bei Funktionsparametern und öffentlichen Schnittstellen, wo kein Anfangswert vorliegt.

</details>

<details>
<summary>Warum ist `any` mit Vorsicht zu verwenden?</summary>

`any` schaltet die Typprüfung für diesen Wert komplett aus - der Compiler kann dann keine Fehler mehr erkennen, die er sonst gefunden hätte.

</details>

---

## Basistypen im Überblick

```ts
let title: string = "Setup Repo";
let priority: number = 1;
let isDone: boolean = false;
let tags: string[] = ["setup", "git"];
let unknownValue: unknown = fetchExternalValue();
```

| Typ       | Beispiel                                                       |
| --------- | -------------------------------------------------------------- |
| `string`  | `"Setup Repo"`                                                 |
| `number`  | `1`                                                            |
| `boolean` | `false`                                                        |
| `T[]`     | `string[]`                                                     |
| `unknown` | Wert unbekannten Typs, muss vor Nutzung geprüft/verengt werden |

**`unknown` vs. `any`:** `unknown` erlaubt keine Operation ohne vorherige Typprüfung - deutlich sicherer als `any`.

**Vorgriff auf Lab 7.3:** der `Ticket`-Status wird später nicht als `string` oder `unknown`, sondern als String-Literal-Union (`"To Do" | "In Progress" | "Done"`) typisiert - eine dritte Möglichkeit, die enger ist als `unknown` (geprüfter Wert) und enger als `string` (nur diese drei Werte statt beliebiger Zeichenketten).

---

## Type Inference

```ts
let count = 3; // TypeScript leitet ab: number
count = "drei"; // Fehler: Type 'string' is not assignable to type 'number'
```

**Grenze:** Inference funktioniert nur, wenn ein Anfangswert vorliegt - Funktionsparameter ohne Typangabe werden sonst implizit `any` (bei `strict: true` als Fehler markiert).

---

## Checkpoint

Ein Beispielwert je Basistyp wurde deklariert; ein absichtlicher Typkonflikt wurde erkannt und korrigiert.

Weiter geht es mit Lab 7.2: Interfaces.
