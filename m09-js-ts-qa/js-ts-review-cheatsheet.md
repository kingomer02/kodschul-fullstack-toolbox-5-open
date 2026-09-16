# JS/TS-Review-Cheatsheet

Kompakte Wiederholung für Modul 9 (Puffer für offene Fragen) - Details siehe [`m06-typescript-intro/typescript-cheatsheet.md`](../m06-typescript-intro/typescript-cheatsheet.md).

## Häufige Stolperstellen im Überblick

| Thema                          | Kurzregel                                                                                |
| ------------------------------ | ---------------------------------------------------------------------------------------- |
| `interface` vs. `type`         | `interface` für Objektformen (erweiterbar), `type` u. a. für Unions (`"A" \| "B"`)       |
| `any` vs. `unknown`            | `any` schaltet Prüfung aus (vermeiden), `unknown` erzwingt Prüfung vor Verwendung        |
| `public`/`protected`/`private` | Standard `public`; `protected` = Klasse + Unterklassen; `private` = nur eigene Klasse    |
| Generics (`<T>`)               | wiederverwendbare, typsichere Klassen/Funktionen statt `any` oder Code-Duplikation       |
| `strict: true`                 | sollte in jedem neuen Projekt aktiv sein, deckt u. a. `null`/`undefined`-Fehler früh auf |

## Schnelltest-Fragen für die Selbstprüfung

1. Warum kompiliert `let x: unknown = "a"; x.toUpperCase();` nicht ohne vorherige Prüfung?
2. Wann liefert `super.methode()` in einer Kindklasse einen Mehrwert gegenüber vollständigem Überschreiben?
3. Warum braucht `class Repository<T extends { id: string }>` die Einschränkung `extends { id: string }`?

## Nächste Schritte

Offene Punkte, die erst mit mehr Kontext beantwortbar sind (z. B. Zusammenspiel mit Docker/APIs), werden ab Modul 10 wieder aufgegriffen.
