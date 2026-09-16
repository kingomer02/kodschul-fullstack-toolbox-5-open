# Lab 6.2 - Übung: `tsconfig.json`-Setup

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - das Backend erhält ein echtes TypeScript-Build-Setup.

## Ausgangslage

`backend/package.json` mit `typescript`/`@types/node` als `devDependencies` existiert (Lab 5.2).

## Aufgaben

1. Erzeuge im `backend/`-Ordner eine `tsconfig.json` mit `npx tsc --init` und passe sie gemäß den Beispielwerten an (`target`, `module`, `rootDir`, `outDir`, `strict`).
2. Lege `backend/src/index.ts` mit einer einzeiligen `console.log("TeamBoard backend starting...")` an.
3. Ergänze in `backend/package.json` die Skripte `build` (`tsc`) und `start` (`node dist/index.js`).
4. Führe `npm run build` und danach `npm run start` aus und prüfe die Ausgabe.

## Checkpoint

- `dist/index.js` wird nach `npm run build` erzeugt.
- `npm run start` gibt die erwartete Konsolenzeile aus.

## Abschlusskriterien

- `backend/dist/` ist über `.gitignore` vom Commit ausgeschlossen (nur `src/` wird versioniert).

## Fallback

Bei Unsicherheit über einzelne `tsconfig`-Optionen: die vom Trainer bereitgestellte Referenz-`tsconfig.json` als Vorlage übernehmen und einzelne Werte gezielt anpassen statt alles neu zu tippen.
