# Modul 8: Objektorientierung in TypeScript

## Lab 8.2 - Access Modifiers

---

## Lab-Ziel

Du kannst `public`, `private` und `protected` gezielt einsetzen, um den Zugriff auf Klasseneigenschaften zu steuern.

**Leitfragen:**

<details>
<summary>Was ist der Unterschied zwischen `public`, `private` und `protected`?</summary>

`public` (Standard) ist überall zugreifbar; `private` nur innerhalb derselben Klasse; `protected` innerhalb der Klasse und ihrer Unterklassen.

</details>

<details>
<summary>Warum überhaupt Zugriff einschränken, wenn der Code am Ende zu JavaScript kompiliert wird?</summary>

Zur Kompilierzeit verhindert es versehentlichen Zugriff/Änderung von außen und macht die beabsichtigte Schnittstelle einer Klasse explizit - auch wenn zur Laufzeit (in reinem JS) keine echte Kapselung existiert.

</details>

<details>
<summary>Wie hängen Access Modifiers mit `TicketRepository`/`TicketService` zusammen?</summary>

Die interne Ticket-Liste sollte `private` sein, damit nur die eigenen Methoden (`add`, `findById`, ...) sie verändern - Außencode darf nur über diese Methoden zugreifen.

</details>

---

## Access Modifiers im Vergleich

```ts
class TicketRepository {
  private tickets: Ticket[] = [];

  add(ticket: Ticket): void {
    this.tickets.push(ticket);
  }

  findById(id: string): Ticket | undefined {
    return this.tickets.find((t) => t.id === id);
  }
}
```

| Modifier            | Zugriff innerhalb Klasse | Zugriff in Unterklasse | Zugriff von außen |
| ------------------- | ------------------------ | ---------------------- | ----------------- |
| `public` (Standard) | Ja                       | Ja                     | Ja                |
| `protected`         | Ja                       | Ja                     | Nein              |
| `private`           | Ja                       | Nein                   | Nein              |

---

## Fehlerbeispiel

```ts
const repo = new TicketRepository();
repo.tickets; // Fehler: Property 'tickets' is private and only accessible within class 'TicketRepository'.
```

Stattdessen muss über die öffentlichen Methoden zugegriffen werden (`repo.add(...)`, `repo.findById(...)`).

---

## Checkpoint

Eine Klasse mit einer `private` internen Liste und ausschließlich öffentlichen Zugriffsmethoden wurde geschrieben; direkter Außenzugriff auf die private Eigenschaft wurde als Fehler bestätigt.

Weiter geht es mit Lab 8.3: Einstieg in Generics.
