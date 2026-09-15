# Lab 2.2 - Lösung: Lokales Repo für das Kursprojekt anlegen

## Aufgabe 1-2: Repo und `.gitignore`

```bash
mkdir teamboard && cd teamboard
git init
cat > .gitignore << 'EOF'
node_modules/
dist/
.env
EOF
```

## Aufgabe 3: `index.html`

```html
<!DOCTYPE html>
<html lang="de">
  <head>
    <meta charset="UTF-8" />
    <title>TeamBoard</title>
  </head>
  <body>
    <h1>TeamBoard</h1>
    <p>Kanban-Ticket-System - wird im Kursverlauf aufgebaut.</p>
  </body>
</html>
```

## Aufgabe 4-5: README kopieren und committen

```bash
cp ../README-draft.md .
git add .gitignore index.html README-draft.md
git commit -m "Initiales TeamBoard-Grundgerüst (HTML + Konzept)"
```

Erwarteter Zustand:

```bash
git log --oneline
# z. B. a1b2c3d Initiales TeamBoard-Grundgerüst (HTML + Konzept)
git status
# nothing to commit, working tree clean
```

## Grenzen

`index.html` ist ein statischer Platzhalter - er wird erst ab Modul 17/18 durch das echte responsive UI bzw. die React-App ersetzt.
