# Transfer-Übung Modul 6 - Übung: Vollständiger Umstieg auf TypeScript

**Dauer:** ca. 15 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - ersetzt den JavaScript-Platzhalter endgültig durch TypeScript und schließt die CI-Anbindung.

## Ziel

Sicherstellen, dass nach Modul 6 wirklich **nur noch** TypeScript-Code im Backend liegt und die bereits bestehende CI-Pipeline (Modul 4) diesen auch tatsächlich prüft.

## Ausgangslage

- `backend/tsconfig.json` und `backend/src/index.ts` aus Lab 6.2 liegen vor; die CI-Skripte wurden bereits auf echten `tsc`-Aufruf umgestellt.

## Aufgaben

1. Lösche `backend/src/index.js`, falls es aus Modul 5 noch vorhanden ist (ersetzt durch `index.ts`).
2. Führe lokal `npm run build && npm start` aus und prüfe die Ausgabe.
3. Push den Stand und beobachte in GitHub Actions, dass die Pipeline echten TypeScript-Code kompiliert (nicht mehr `echo`-Platzhalter).
4. Notiere in einem Satz, was dir noch fehlt, um aus `index.ts` einen echten Server zu machen (Vorschau auf Modul 14).

## Checkpoint

- Kein `.js`-Platzhalter mehr im `backend/src/`-Ordner.
- CI-Check auf `main` ist grün und zeigt einen echten `tsc`-Build-Schritt im Log.

## Abschlusskriterien

- Backend ist vollständig TypeScript-first, bereit für typisierte Datenmodelle in Modul 7.

## Fallback

Falls die Pipeline nach dem Push rot wird: `npm run build` lokal ausführen und die von `tsc` gemeldeten Fehlerzeilen zuerst lokal beheben, bevor erneut gepusht wird.
