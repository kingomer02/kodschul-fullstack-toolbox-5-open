# Lab 6.2 - Lösung: `tsconfig.json`-Setup

## Aufgabe 1: `tsconfig.json`

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "commonjs",
    "rootDir": "src",
    "outDir": "dist",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true
  },
  "include": ["src/**/*"]
}
```

## Aufgabe 2: Einstiegsdatei

```ts
// backend/src/index.ts
console.log("TeamBoard backend starting...");
```

## Aufgabe 3: Skripte

```json
{
  "scripts": {
    "build": "tsc",
    "start": "node dist/index.js"
  }
}
```

## Aufgabe 4: Ausführen

```bash
npm run build
npm run start
# TeamBoard backend starting...
```

## `.gitignore`-Ergänzung

```text
dist/
```

## Grenzen

`index.ts` enthält noch keine echte Serverlogik - Express kommt erst mit der REST-API in Modul 14 dazu.
