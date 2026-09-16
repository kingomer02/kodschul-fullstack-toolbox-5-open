# Lab 19.2 - Lösung: Datenfluss: Login, Token und echte Tickets laden

## Aufgabe 1: CORS aktivieren

```bash
cd backend
npm install cors
npm install --save-dev @types/cors
```

```ts
// backend/src/index.ts (Ausschnitt, vor den Routen)
import cors from "cors";

app.use(cors());
```

## Aufgabe 2: Neu bauen

```bash
docker compose up -d --build
```

## Aufgabe 3-5: `LoginForm` und `App.tsx`

Siehe vollständigen Code im Theorieteil (Lab 19.2, Abschnitte "Login-Formular mit State" und "Echte Tickets laden").

## Aufgabe 6: Testnutzer registrieren und einloggen

```bash
curl -X POST http://localhost:3000/auth/register \
  -H "Content-Type: application/json" -d '{"username": "alex", "password": "hunter2"}'
```

Im Browser (`npm run dev` im `frontend/`-Ordner): Formular mit `alex`/`hunter2` ausfüllen und absenden.

## Aufgabe 7: Prüfen

```bash
curl -X POST http://localhost:3000/tickets \
  -H "Authorization: Bearer <token>" -H "Content-Type: application/json" \
  -d '{"title": "Über curl angelegt"}'
```

Nach einem erneuten Login im Browser erscheint "Über curl angelegt" in der "To Do"-Spalte.

## Grenzen

Der Token wird hier nur im React-State gehalten - bei einem Neuladen der Seite (F5) ist er weg und ein erneuter Login nötig. `localStorage` als dauerhaftere Alternative ist eine mögliche, hier nicht verpflichtende Erweiterung.
