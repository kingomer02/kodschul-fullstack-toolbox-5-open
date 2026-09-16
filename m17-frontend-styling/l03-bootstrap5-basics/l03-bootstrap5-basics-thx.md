# Modul 17: Frontend-Styling

## Lab 17.3 - Bootstrap 5: Grundlagen für die TeamBoard-Oberfläche

---

## Lab-Ziel

Du kannst mit Bootstrap-5-Klassen ein responsives Grundgerüst für das TeamBoard-Kanban-Board bauen, ohne eigenes CSS für das Grundlayout zu schreiben.

**Leitfragen:**

<details>
<summary>Was übernimmt Bootstrap, das man in Lab 17.2 noch selbst mit Grid/Flexbox geschrieben hat?</summary>

Bootstrap liefert fertige, getestete Klassen (`.row`, `.col`, `.container`) für responsive Layouts - man beschreibt die Struktur über Klassen, statt eigenes Grid-/Flexbox-CSS zu schreiben.

</details>

<details>
<summary>Warum reicht ein einzelnes `<link>`-Tag im `<head>`, um Bootstrap zu nutzen?</summary>

Bootstrap wird hier über ein CDN als fertiges CSS eingebunden - der Browser lädt die komplette Bibliothek direkt, ohne dass ein eigener Build-Schritt nötig ist.

</details>

---

## Bootstrap per CDN einbinden

```html
<!-- frontend/index.html -->
<!DOCTYPE html>
<html lang="de">
  <head>
    <meta charset="UTF-8" />
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
      rel="stylesheet"
    />
    <title>TeamBoard</title>
  </head>
  <body>
    <div class="container-fluid">
      <div class="row">
        <div class="col-12 col-md-4">
          <h2>To Do</h2>
          <div class="card mb-2">
            <div class="card-body">Ticket A</div>
          </div>
        </div>
        <div class="col-12 col-md-4">
          <h2>In Progress</h2>
        </div>
        <div class="col-12 col-md-4">
          <h2>Done</h2>
        </div>
      </div>
    </div>
  </body>
</html>
```

- `col-12 col-md-4`: auf kleinen Bildschirmen volle Breite (12 von 12 Spalten), ab "medium" (≥768px) je ein Drittel (4 von 12 Spalten) - Bootstraps eigenes Breakpoint-System übernimmt, was in Lab 17.2 noch eine manuelle `@media`-Regel war.

---

## Checkpoint

Auf einem schmalen Bildschirm stehen die drei Spalten untereinander; ab "medium"-Breite stehen sie nebeneinander - ganz ohne eigenes `@media`.

## Projektbezug

Weiter geht es mit Lab 17.4: eigenes Sass für Farben und Abstände, die über Bootstraps Grundgerüst hinausgehen.
