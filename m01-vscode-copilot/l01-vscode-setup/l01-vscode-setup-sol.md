# Lab 1.1 - Lösung: VS Code Konfiguration und Erweiterungen

## Aufgabe 1: Erweiterungen installieren

Über die Extensions-Ansicht (Cmd/Ctrl+Shift+X) nach `ESLint`, `Prettier - Code formatter`, `Docker` und `GitLens` suchen und installieren. Nach der Installation erscheinen die Icons in der Aktivitätsleiste.

## Aufgabe 2: `.vscode/settings.json`

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "files.eol": "\n"
}
```

Diese Datei liegt im Projekt (nicht im User-Profil), damit sie für alle Teilnehmer gleich wirkt, sobald sie den Ordner öffnen.

## Aufgabe 3: Automatische Formatierung beobachten

```js
function add(a, b) {
  return a + b;
}
```

Nach dem Speichern formatiert Prettier automatisch zu:

```js
function add(a, b) {
  return a + b;
}
```

Grund: `editor.formatOnSave` löst bei jedem Speichern den in `editor.defaultFormatter` konfigurierten Formatter aus.

## Aufgabe 4: Versionsprüfung

Erwartete Beispielausgaben (Versionsnummern variieren je nach lokaler Installation):

```text
$ node -v
v20.11.0
$ git --version
git version 2.43.0
$ docker --version
Docker version 25.0.3
```

Ein Fehler wie `command not found` bedeutet, dass die jeweilige Software fehlt oder nicht im `PATH` liegt - das ist der offene Punkt, der vor Modul 10 gelöst werden muss.

## Grenzen

Diese Übung prüft nur, dass die Tools lokal aufrufbar sind, nicht ihre vollständige Konfiguration (z. B. Docker-Ressourcenlimits). Das wird im Docker-Modul (Tag 3) vertieft.
