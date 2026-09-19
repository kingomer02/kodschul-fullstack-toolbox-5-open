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
5. Ersetze in `backend/package.json` die Platzhalter-Skripte aus Modul 4 (`"lint": "echo ..."`, `"build": "echo ..."`) durch `"lint": "tsc --noEmit"` und `"build": "tsc"`. **Ergänze dann in `.github/workflows/ci.yml` bei den Schritten `npm ci`, `npm run lint` und `npm run build` jeweils `working-directory: backend`**, committe und pushe, und prüfe im Actions-Tab, dass die Pipeline weiterhin grün ist.

> **Korrektur (Durchlauf 09/2026, Ö. Akgeyik):** Ohne diese Ergänzung prüft die Pipeline weiterhin die Platzhalter im Wurzelverzeichnis: Die Skripte werden in `backend/package.json` ersetzt, der Workflow aus Modul 4 läuft aber im Root. Die CI bliebe grün, ohne TypeScript je kompiliert zu haben - der schlimmste Fall, weil er wie Erfolg aussieht.

## Checkpoint

- `dist/index.js` wird nach `npm run build` erzeugt.
- `npm run start` gibt die erwartete Konsolenzeile aus.

## Abschlusskriterien

- `backend/dist/` ist über `.gitignore` vom Commit ausgeschlossen (nur `src/` wird versioniert).

## Fallback

Bei Unsicherheit über einzelne `tsconfig`-Optionen: die vom Trainer bereitgestellte Referenz-`tsconfig.json` als Vorlage übernehmen und einzelne Werte gezielt anpassen statt alles neu zu tippen.
