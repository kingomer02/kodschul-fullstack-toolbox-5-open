# Lab 17.3 - Lösung: Bootstrap 5: Grundlagen für die TeamBoard-Oberfläche

## Aufgabe 1-3: `frontend/index.html`

```html
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
          <div class="card mb-2">
            <div class="card-body">Ticket B</div>
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

## Aufgabe 4: Testen

Im responsiven Modus bei 375px stehen die Spalten untereinander; ab 768px (Bootstraps `md`-Breakpoint) stehen sie nebeneinander.

## Aufgabe 5: Commit

```bash
git add frontend/index.html
git commit -m "feat: add Bootstrap-based frontend skeleton"
```

## Grenzen

Dieses Grundgerüst ist reines, statisches HTML - es lädt noch keine echten Tickets von der API. Das folgt in Modul 19.
