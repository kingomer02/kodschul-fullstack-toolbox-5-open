# Modul 7: TypeScript-Grundlagen

## Lab 7.2 - Interfaces

---

## Lab-Ziel

Du kannst ein `interface` definieren und damit die Form eines Objekts verbindlich beschreiben.

**Leitfragen:**

<details>
<summary>Was beschreibt ein `interface`?</summary>

Die erwartete Form (Struktur) eines Objekts - welche Eigenschaften mit welchem Typ vorhanden sein müssen.

</details>

<details>
<summary>Was passiert, wenn ein Objekt nicht zum `interface` passt?</summary>

Der Compiler meldet einen Fehler, sobald das Objekt einer Variable/einem Parameter dieses Typs zugewiesen wird - fehlende, zusätzliche oder falsch typisierte Eigenschaften werden erkannt.

</details>

<details>
<summary>Wie macht man eine Eigenschaft optional?</summary>

Mit einem `?` nach dem Eigenschaftsnamen, z. B. `description?: string`.

</details>

---

## Ein `interface` definieren

```ts
interface Person {
  name: string;
  age: number;
  email?: string;
}

const alex: Person = { name: "Alex", age: 29 };
const sam: Person = { name: "Sam", age: 31, email: "sam@example.com" };
```

**Grenze:** ein `interface` existiert nur zur Kompilierzeit - es hat keine Auswirkung auf den erzeugten JavaScript-Code.

---

## Fehlerbeispiel

```ts
const invalid: Person = { name: "Jo" };
// Fehler: Property 'age' is missing in type '{ name: string; }' but required in type 'Person'.
```

---

## `interface` vs. `type`

| Merkmal                                             | `interface`  | `type`  |
| --------------------------------------------------- | ------------ | ------- |
| Erweiterbar (mehrere Deklarationen zusammengeführt) | Ja           | Nein    |
| Für Objektformen                                    | üblich       | möglich |
| Für Unions (`"A" \| "B"`)                           | nicht direkt | üblich  |

**Für diesen Kurs:** Objektformen (`Ticket`, `Person`) als `interface`, Status-Werte als String-Union-`type` (siehe Lab 7.3).

---

## Checkpoint

Ein `interface` mit mindestens einer optionalen Eigenschaft wurde definiert; ein absichtlich unvollständiges Objekt wurde als Fehler erkannt.

Weiter geht es mit Lab 7.3: Datenmodelle typisieren.
