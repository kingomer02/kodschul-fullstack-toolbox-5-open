# Lab 1.1 - Übung: VS Code Konfiguration und Erweiterungen

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - Setup-Übung, kein Projektcode.

## Ausgangslage

Du startest mit einer Standard-VS-Code-Installation ohne kursspezifische Konfiguration.

## Vorbereitung

- VS Code ist installiert und startet fehlerfrei.
- Ein leerer Ordner `vscode-setup-uebung/` liegt lokal bereit.

## Aufgaben

1. Installiere die vier Kurs-Erweiterungen: ESLint, Prettier, Docker, GitLens.
2. Lege im Ordner `vscode-setup-uebung/` eine Datei `.vscode/settings.json` mit `editor.formatOnSave: true` und `editor.defaultFormatter` auf Prettier an.
3. Lege eine Datei `beispiel.js` mit inkonsistenter Formatierung an (z. B. unterschiedliche Einrückung) und speichere sie. Beobachte, was passiert.
4. Öffne ein VS-Code-Terminal und führe `node -v`, `git --version`, `docker --version` aus. Notiere die Ausgaben.

## Checkpoint

- `beispiel.js` wird nach dem Speichern automatisch von Prettier formatiert.
- Alle drei Versionskommandos liefern eine Versionsnummer statt eines Fehlers.

## Abschlusskriterien

- `.vscode/settings.json` existiert mit den genannten zwei Einstellungen.
- Formatierung greift nachweislich beim Speichern.

## Fallback

Falls Docker Desktop noch nicht installiert ist: fahre mit den übrigen Aufgaben fort und installiere Docker bis spätestens Modul 10 (Tag 3) nach - das Modul beginnt mit einem erneuten Setup-Check.
