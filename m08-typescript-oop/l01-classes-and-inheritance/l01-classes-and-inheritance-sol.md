# Lab 8.1 - Lösung: Klassen und Vererbung

## Aufgabe 1: Basisklasse

```ts
class Notification {
  constructor(protected message: string) {}

  send(): string {
    return `Notification: ${this.message}`;
  }
}
```

## Aufgabe 2-3: Abgeleitete Klasse

```ts
class EmailNotification extends Notification {
  constructor(message: string, private recipient: string) {
    super(message);
  }

  send(): string {
    return `${super.send()} -> to ${this.recipient}`;
  }
}
```

## Aufgabe 4: Instanziieren und aufrufen

```ts
const generic = new Notification("Build finished");
console.log(generic.send()); // Notification: Build finished

const email = new EmailNotification("Build finished", "alex@example.com");
console.log(email.send()); // Notification: Build finished -> to alex@example.com
```

## Grenzen

`message` ist hier `protected`, damit die Kindklasse zugreifen kann - ein vollständiger Vergleich der Access Modifiers folgt in Lab 8.2.
