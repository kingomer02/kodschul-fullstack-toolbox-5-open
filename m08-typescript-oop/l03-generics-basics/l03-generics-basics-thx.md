# Modul 8: Objektorientierung in TypeScript

## Lab 8.3 - Einstieg in Generics

---

## Lab-Ziel

Du verstehst, warum Generics eine wiederverwendbare, typsichere `Repository`-Klasse ermöglichen, und hast `TicketRepository` darauf umgestellt.

**Leitfragen:**

<details>
<summary>Welches Problem lösen Generics?</summary>

Ohne Generics müsste für jeden Datentyp eine eigene, fast identische Klasse geschrieben werden (oder `any` verwendet werden, was Typsicherheit aufgibt); Generics erlauben eine Klasse/Funktion, die mit einem Platzhaltertyp `T` für beliebige konkrete Typen funktioniert.

</details>

<details>
<summary>Was bedeutet `class Repository<T>`?</summary>

`T` ist ein Typparameter - beim tatsächlichen Gebrauch (`new Repository<Ticket>()`) wird `T` durch einen konkreten Typ ersetzt, und alle Methoden werden entsprechend typsicher.

</details>

<details>
<summary>Wo in TeamBoard könnte eine generische `Repository<T>` später wiederverwendet werden?</summary>

Für andere Entitäten als `Ticket` (z. B. Nutzerkonten für die Authentifizierung in Modul 16), ohne die Repository-Logik erneut zu schreiben.

</details>

---

## Eine generische Klasse

```ts
class Repository<T extends { id: string }> {
  private items: T[] = [];

  add(item: T): void {
    this.items.push(item);
  }

  findById(id: string): T | undefined {
    return this.items.find((item) => item.id === id);
  }
}
```

- `T extends { id: string }` schränkt `T` auf Typen mit mindestens einer `id: string`-Eigenschaft ein - nötig, damit `findById` funktioniert.

---

## Konkrete Nutzung

```ts
const ticketRepo = new Repository<Ticket>();
ticketRepo.add({
  id: "t-1",
  title: "Setup Repo",
  description: "Initial repo structure",
  assignee: "Alex",
  status: "To Do",
});

const found = ticketRepo.findById("t-1"); // Typ: Ticket | undefined
```

**Grenze:** ohne die Einschränkung `extends { id: string }` würde `findById` nicht kompilieren, weil TypeScript nicht wüsste, dass `item.id` existiert.

---

## Checkpoint

`TicketRepository` wurde durch eine generische `Repository<T>` ersetzt oder darauf aufgebaut und mit `Ticket` als konkretem Typ verwendet; das Verhalten aus Lab 8.2 bleibt unverändert.

Weiter geht es mit Modul 9: Puffer für offene JavaScript/TypeScript-Fragen.
