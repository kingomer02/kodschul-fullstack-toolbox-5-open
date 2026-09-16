# Lab 18.3 - Lösung: React-Projekt-Setup für TeamBoard

## Aufgabe 1: Sicherung

```bash
cp frontend/styles/main.scss /tmp/main.scss.backup
mv frontend frontend-static-backup
```

## Aufgabe 2: Vite-Projekt einrichten

```bash
npm create vite@latest frontend -- --template react-ts
cd frontend
npm install
npm install bootstrap
```

## Aufgabe 3: Styles übernehmen

```bash
mkdir -p src/styles
cp /tmp/main.scss.backup src/styles/main.scss
```

```ts
// frontend/src/main.tsx (Ausschnitt)
import "bootstrap/dist/css/bootstrap.min.css";
import "./styles/main.scss";
```

## Aufgabe 4-6: Komponenten und `App.tsx`

Siehe vollständigen Code im Theorieteil (Lab 18.3, Abschnitt "Vollständiges Board rendern") sowie `TicketCard`/`Column` aus Lab 18.2.

## Aufgabe 7: Testen

```bash
npm run dev
# http://localhost:5173 zeigt das Drei-Spalten-Board mit Modul-17-Styling
```

## Aufgabe 8: Commit

```bash
rm -rf frontend-static-backup
git add -A
git commit -m "feat: set up Vite React frontend with Bootstrap and Sass from module 17"
```

## Grenzen

Die Beispieldaten in `sample-tickets.ts` sind weiterhin statisch im Code hinterlegt - eine echte Verbindung zur MongoDB-gestützten API folgt erst in Modul 19.
