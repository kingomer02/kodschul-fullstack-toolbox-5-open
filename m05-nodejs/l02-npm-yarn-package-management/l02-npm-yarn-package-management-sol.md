# Lab 5.2 - Lösung: NPM/Yarn-Paketmanagement

## Aufgabe 1: Projekt initialisieren

```bash
mkdir backend && cd backend
npm init -y
```

## Aufgabe 2: Pakete installieren

```bash
npm install express
npm install --save-dev typescript @types/node
```

Ausschnitt aus `backend/package.json`:

```json
{
  "dependencies": {
    "express": "^4.19.2"
  },
  "devDependencies": {
    "typescript": "^5.4.0",
    "@types/node": "^20.11.0"
  }
}
```

## Aufgabe 3: `.gitignore`

```text
node_modules/
dist/
.env
```

## Aufgabe 4: Commit

```bash
git add backend/package.json backend/package-lock.json .gitignore
git commit -m "chore: init backend Node.js project"
```

## Grenzen

`express` wird hier nur installiert, nicht verwendet - ein lauffähiger Server folgt erst mit dem TypeScript-Setup (Modul 6) und der REST-API (Modul 14).
