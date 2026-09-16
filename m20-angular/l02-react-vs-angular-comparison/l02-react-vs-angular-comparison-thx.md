# Modul 20: Angular im Vergleich (Trainer-Demo)

## Lab 20.2 - React versus Angular: Vergleich

---

## Lab-Ziel

Du kannst für ein gegebenes Kriterium (z. B. Lernkurve, Struktur, Ökosystem) begründet einschätzen, ob React oder Angular in diesem konkreten Aspekt eher zusagt.

**Hinweis:** Dieses Lab ist eine reine Trainer-Demo ohne eigene Teilnehmerübung.

---

## Vergleichstabelle

| Kriterium              | React (Modul 18/19)                           | Angular                                     |
| ---------------------- | --------------------------------------------- | ------------------------------------------- |
| Typ                    | Bibliothek (UI-Schicht)                       | vollständiges Framework                     |
| Sprache                | JavaScript/TypeScript, JSX                    | TypeScript verpflichtend, HTML-Templates    |
| Struktur               | freie Wahl (Router, State-Management separat) | vorgegebene Struktur (Module, Services, DI) |
| Datenbindung           | einseitig (`useState` + manuelles Rendern)    | zweiseitig möglich (`[(ngModel)]`)          |
| Einstieg für TeamBoard | wurde in Modul 18/19 genutzt                  | hier nur als Konzept-Demo gezeigt           |

**Grenze:** Diese Tabelle ist bewusst vereinfacht - beide Ökosysteme entwickeln sich weiter und einzelne Aussagen (z. B. zu State-Management) können sich je nach gewählten Zusatzbibliotheken relativieren.

---

## TeamBoard-Perspektive

TeamBoard wurde in Modul 18/19 bewusst mit React umgesetzt, weil:

- der Kurs bereits mit einer flexiblen, bibliotheksbasierten Herangehensweise (Express statt eines vorgegebenen Backend-Frameworks) begonnen hat,
- React für den in diesem Kurs gezeigten Umfang (drei Spalten, wenige Komponenten) ohne zusätzliche Angular-Konzepte wie Dependency Injection auskommt.

Ein mit Angular umgesetztes TeamBoard wäre technisch ebenso möglich, hätte aber mehr anfängliche Struktur (Module, Services) vorausgesetzt.

---

## Live-Demo-Ablauf (durch den Trainer)

1. Denselben `TicketCardComponent`-Ausschnitt aus Lab 20.1 neben die React-`TicketCard`-Komponente aus Modul 18 legen und Zeile für Zeile vergleichen.
2. Eine offene Frage aus der Gruppe aufgreifen (z. B. "Wann würde ich Angular statt React wählen?") und anhand der Tabelle live diskutieren.

## Checkpoint

Die Teilnehmenden können mindestens ein Kriterium nennen, bei dem sie React bevorzugen würden, und eines, bei dem Angular Vorteile bietet.

## Projektbezug

Dieser Vergleich schließt den SPA-Teil des Kurses ab. Modul 21 zeigt als weitere Demo, wie eine solche SPA in Azure bereitgestellt werden könnte.
