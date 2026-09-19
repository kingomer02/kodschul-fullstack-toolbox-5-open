# Lab 8.1 - Übung: Klassen und Vererbung

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - generische Übung; `TicketRepository` folgt in Lab 8.2/8.3.

## Ausgangslage

Ein lauffähiges TypeScript-Setup existiert (Modul 6).

## Aufgaben

1. Schreibe eine Klasse `Notification` mit Konstruktor-Parameter `message: string` und einer Methode `send(): string`, die die Nachricht zurückgibt.

> **Achtung:** `class Notification` kollidiert mit dem gleichnamigen Browser-Typ und bricht mit `TS2300: Duplicate identifier 'Notification'` ab, sobald die DOM-Typen geladen sind. Setzt in der `tsconfig.json` unter `compilerOptions` **`"lib": ["ES2022"]`** - damit werden die DOM-Typen nicht eingebunden. Wer die DOM-Typen braucht, benennt die Klasse um, z. B. in `AppNotification`.
2. Leite `EmailNotification extends Notification` ab, die zusätzlich einen `recipient: string` im Konstruktor entgegennimmt.
3. Überschreibe `send()` in `EmailNotification` so, dass sie `super.send()` nutzt und den Empfänger ergänzt.
4. Instanziiere beide Klassen und rufe jeweils `send()` auf.

## Checkpoint

- `EmailNotification.send()` enthält sowohl die Basisnachricht (via `super.send()`) als auch den Empfänger.

## Abschlusskriterien

- Beide Klassen kompilieren fehlerfrei (`npx tsc --noEmit`).

## Fallback

Bei Unsicherheit über `super()`: zunächst ohne Vererbung zwei unabhängige Klassen schreiben, danach gezielt die gemeinsame Basis extrahieren.
