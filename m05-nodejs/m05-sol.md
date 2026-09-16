# Transfer-Übung Modul 5 - Lösung: Lauffähiges Backend-Platzhalterskript

## Aufgabe 1-3: Skript anlegen und ausführen

```bash
cd backend
mkdir -p src
echo 'console.log("TeamBoard backend placeholder");' > src/index.js
npm pkg set scripts.start="node src/index.js"
npm start
# TeamBoard backend placeholder
```

## Aufgabe 4: Commit

```bash
git add package.json src/index.js
git commit -m "feat: add runnable backend placeholder script"
```

## Grenzen

`src/index.js` ist ein reiner Platzhalter - in Modul 6 wird er durch `src/index.ts` ersetzt.
