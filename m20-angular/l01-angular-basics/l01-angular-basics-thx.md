# Modul 20: Angular im Vergleich (Trainer-Demo)

## Lab 20.1 - Angular-Grundkonzepte

---

## Lab-Ziel

Du kennst die zentralen Bausteine eines Angular-Projekts (Komponenten, Templates, Module, TypeScript-Dekoratoren) auf einem Niveau, das einen fundierten Vergleich zu React erlaubt.

**Hinweis:** Dieses Lab ist eine reine Trainer-Demo ohne eigene Teilnehmerübung - der Fokus liegt auf dem Verständnis der Konzepte, nicht auf eigenem Programmieren.

---

## Angular-Komponente im Überblick

```ts
// demo-angular/src/app/ticket-card/ticket-card.component.ts
import { Component, Input } from "@angular/core";

@Component({
  selector: "app-ticket-card",
  template: `
    <div class="card mb-2">
      <div class="card-body">
        <p>{{ title }}</p>
        <small>{{ assignee || "Nicht zugewiesen" }}</small>
      </div>
    </div>
  `,
})
export class TicketCardComponent {
  @Input() title!: string;
  @Input() assignee!: string;
}
```

- `@Component` ist ein **Dekorator** - eine TypeScript-Annotation, die eine Klasse zu einer Angular-Komponente macht (vergleichbar in der Rolle, aber syntaktisch anders als eine React-Funktionskomponente).
- `@Input()` markiert eine Eigenschaft als von außen übergebbar - das Gegenstück zu React-Props.
- Das `template` ist HTML mit Angular-spezifischer Syntax (`{{ }}` für Textinterpolation) statt JSX.

## Module statt einzelner Imports

```ts
// demo-angular/src/app/app.module.ts (Ausschnitt)
import { NgModule } from "@angular/core";
import { TicketCardComponent } from "./ticket-card/ticket-card.component";

@NgModule({
  declarations: [TicketCardComponent],
})
export class AppModule {}
```

- Angular gruppiert Komponenten in **Modulen** (`NgModule`) - React kennt dieses Konzept nicht, dort werden Komponenten einfach direkt importiert und verwendet.

---

## Live-Demo-Ablauf (durch den Trainer)

1. Ein neues Angular-Projekt live erzeugen (`ng new demo-angular`) und den Ordnerbaum zeigen.
2. Eine einfache `TicketCardComponent` mit `@Input()` live erstellen und in `app.component.html` einbinden.
3. Den Dev-Server starten (`ng serve`) und das Ergebnis im Browser zeigen.

## Checkpoint

Die Teilnehmenden können nach der Demo die drei Begriffe `@Component`, `@Input()` und `NgModule` jeweils einem React-Konzept aus Modul 18 zuordnen (Komponente, Props, "kein direktes Gegenstück").

Weiter geht es mit Lab 20.2: React und Angular im direkten Vergleich.
