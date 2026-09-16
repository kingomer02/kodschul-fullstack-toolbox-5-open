# Modul 17: Frontend-Styling

## Lab 17.4 - Sass-Grundlagen für eigene Farben und Abstände

---

## Lab-Ziel

Du kannst mit Sass-Variablen und Verschachtelung eigenes CSS für TeamBoard-spezifische Farben und Abstände schreiben, das über Bootstraps Standardaussehen hinausgeht.

**Leitfragen:**

<details>
<summary>Was ist der Vorteil einer Sass-Variable wie `$todo-color` gegenüber einem wiederholt eingetippten Farbwert?</summary>

Eine Änderung des Werts an einer Stelle wirkt sich auf alle Verwendungen aus - bei wiederholten Farbwerten müsste man jede Stelle einzeln suchen und anpassen.

</details>

<details>
<summary>Was bedeutet Verschachtelung (`&`) in Sass am Beispiel `.ticket { &:hover { ... } }`?</summary>

`&` steht für den umgebenden Selektor - das Ergebnis entspricht `.ticket:hover { ... }` in normalem CSS, aber ohne den Selektornamen zu wiederholen.

</details>

---

## Sass-Datei mit Variablen und Verschachtelung

```scss
// frontend/styles/main.scss
$todo-color: #f0ad4e;
$in-progress-color: #5bc0de;
$done-color: #5cb85c;
$ticket-radius: 6px;

.column {
  padding: 0.5rem;

  &.todo {
    border-top: 4px solid $todo-color;
  }

  &.in-progress {
    border-top: 4px solid $in-progress-color;
  }

  &.done {
    border-top: 4px solid $done-color;
  }
}

.ticket {
  border-radius: $ticket-radius;

  &:hover {
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.15);
  }
}
```

- Die Kompilierung zu normalem CSS übernimmt Lab 17.5 mit Gulp - hier steht bewusst noch nur die `.scss`-Quelldatei.

---

## Checkpoint

Die `.scss`-Datei enthält mindestens drei Variablen und mindestens eine Verschachtelung mit `&` - beides sind Sass-Funktionen, die reines CSS an dieser Stelle nicht anbietet.

## Projektbezug

Weiter geht es mit Lab 17.5: diese `.scss`-Datei automatisiert mit Gulp zu `.css` kompilieren.
