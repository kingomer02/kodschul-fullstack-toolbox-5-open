# Modul 8: Objektorientierung in TypeScript

## Lab 8.1 - Klassen und Vererbung

---

## Lab-Ziel

Du kannst eine Klasse mit Konstruktor und Methoden schreiben und über `extends` eine Kindklasse ableiten.

**Leitfragen:**

<details>
<summary>Was ist der Unterschied zwischen einem `interface` und einer `class`?</summary>

Ein `interface` beschreibt nur die Form, existiert nicht zur Laufzeit; eine `class` erzeugt tatsächliche Objekte (Instanzen) mit Zustand und Verhalten (Methoden).

</details>

<details>
<summary>Was passiert bei `extends`?</summary>

Die Kindklasse übernimmt Eigenschaften und Methoden der Elternklasse und kann eigene ergänzen oder überschreiben.

</details>

<details>
<summary>Wofür wird `super()` im Konstruktor der Kindklasse gebraucht?</summary>

Es ruft den Konstruktor der Elternklasse auf, damit deren Eigenschaften korrekt initialisiert werden, bevor die Kindklasse eigene Initialisierung vornimmt.

</details>

---

## Eine einfache Klasse

```ts
class Repository {
  constructor(public name: string) {}

  describe(): string {
    return `Repository: ${this.name}`;
  }
}

const repo = new Repository("teamboard");
console.log(repo.describe()); // Repository: teamboard
```

---

## Vererbung mit `extends`

```ts
class InMemoryRepository extends Repository {
  private items: string[] = [];

  constructor(name: string) {
    super(name);
  }

  add(item: string): void {
    this.items.push(item);
  }

  describe(): string {
    return `${super.describe()} (${this.items.length} items)`;
  }
}

const inMemory = new InMemoryRepository("teamboard-tickets");
inMemory.add("Setup Repo");
console.log(inMemory.describe()); // Repository: teamboard-tickets (1 items)
```

- `super.describe()` ruft die Methode der Elternklasse auf und ergänzt sie, statt sie komplett zu ersetzen.

---

## Checkpoint

Eine Basisklasse und eine davon abgeleitete Klasse wurden erstellt, instanziiert und liefern beim Aufruf einer überschriebenen Methode das erwartete kombinierte Ergebnis.

Weiter geht es mit Lab 8.2: Access Modifiers.
