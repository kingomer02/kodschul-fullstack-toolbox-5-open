# TypeScript-Cheatsheet

Schnellreferenz für Modul 6-8 (Einführung, Grundlagen, Objektorientierung).

## Compiler-Grundbefehle

| Befehl               | Wirkung                                                |
| -------------------- | ------------------------------------------------------ |
| `npx tsc --init`     | `tsconfig.json` mit Standardoptionen erzeugen          |
| `npx tsc`            | Projekt gemäß `tsconfig.json` kompilieren              |
| `npx tsc <datei>.ts` | einzelne Datei ohne Projektkonfiguration kompilieren   |
| `npx tsc --noEmit`   | nur auf Typfehler prüfen, keine `.js`-Dateien erzeugen |

## Wichtige `tsconfig.json`-Optionen

| Option               | Bedeutung                                    |
| -------------------- | -------------------------------------------- |
| `target`             | erzeugte ECMAScript-Version (z. B. `ES2022`) |
| `module`             | Modulsystem (z. B. `commonjs` für Node.js)   |
| `rootDir` / `outDir` | Quellordner vs. Ausgabeordner                |
| `strict`             | strenge Typprüfung aktivieren (empfohlen)    |
| `esModuleInterop`    | einfacherer Import von CommonJS-Paketen      |

## Basistypen

```ts
let title: string = "Setup Repo";
let priority: number = 1;
let isDone: boolean = false;
let tags: string[] = ["setup", "git"];
let unknownValue: unknown = fetchExternalValue();
```

| Typ                           | Hinweis                             |
| ----------------------------- | ----------------------------------- |
| `string`, `number`, `boolean` | Basiswerte                          |
| `T[]`                         | Array eines Typs                    |
| `unknown`                     | erzwingt Prüfung vor Verwendung     |
| `any`                         | schaltet Typprüfung aus - vermeiden |

## Interfaces

```ts
interface Ticket {
  id: string;
  title: string;
  description: string;
  assignee: string;
  status: "To Do" | "In Progress" | "Done";
  email?: string; // optionale Eigenschaft
}
```

- `?` markiert eine Eigenschaft als optional.
- String-Union (`"A" | "B" | "C"`) statt `string`, wenn nur bestimmte Werte gültig sein sollen.

## Klassen und Vererbung

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

class TicketRepository extends Repository<Ticket> {}
```

## Access Modifiers

| Modifier            | Innerhalb Klasse | Unterklasse | Von außen |
| ------------------- | ---------------- | ----------- | --------- |
| `public` (Standard) | Ja               | Ja          | Ja        |
| `protected`         | Ja               | Ja          | Nein      |
| `private`           | Ja               | Nein        | Nein      |

## Generics

- `class Repository<T>` bzw. `function identity<T>(value: T): T` - `T` wird beim Gebrauch durch einen konkreten Typ ersetzt.
- Einschränkung mit `extends`, z. B. `T extends { id: string }`, wenn der generische Typ bestimmte Eigenschaften garantieren muss.

## Faustregeln

- `strict: true` immer aktivieren, besonders bei neuen Projekten.
- `any` vermeiden, `unknown` + Typprüfung bevorzugen.
- Datenmodelle (`interface`) an einer zentralen Stelle definieren und überall importieren, statt sie mehrfach zu duplizieren.
