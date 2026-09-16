# VS Code & Copilot-Cheatsheet

Schnellreferenz für Modul 1 (VS Code-Konfiguration, Copilot-gestützte Workflows).

## Wichtige VS Code-Kurzbefehle

| Tastenkombination (macOS / Windows-Linux) | Wirkung                                |
| ----------------------------------------- | -------------------------------------- |
| `Cmd+Shift+P` / `Ctrl+Shift+P`            | Command Palette öffnen                 |
| `Cmd+P` / `Ctrl+P`                        | Datei schnell öffnen                   |
| `Cmd+,` / `Ctrl+,`                        | Einstellungen öffnen                   |
| `Cmd+Shift+X` / `Ctrl+Shift+X`            | Extensions-Ansicht öffnen              |
| `` Ctrl+` ``                              | integriertes Terminal öffnen/schließen |
| `Cmd+B` / `Ctrl+B`                        | Seitenleiste ein-/ausblenden           |

## Empfohlene Grundkonfiguration

| Einstellung           | Zweck                                           |
| --------------------- | ----------------------------------------------- |
| `editor.formatOnSave` | Code automatisch beim Speichern formatieren     |
| `files.autoSave`      | automatisches Speichern nach kurzer Inaktivität |
| `editor.tabSize`      | konsistente Einrückung im Team sicherstellen    |

## Copilot Chat - Grundfunktionen

| Aktion       | Wirkung                                                       |
| ------------ | ------------------------------------------------------------- |
| Chat öffnen  | Seitenleiste oder `Cmd+Ctrl+I` / `Ctrl+Alt+I`                 |
| `/explain`   | markierten Code erklären lassen                               |
| `/fix`       | Vorschlag zur Fehlerbehebung für markierten Code              |
| `/tests`     | Testvorschläge für markierten Code generieren                 |
| `@workspace` | Frage mit Kontext aus dem gesamten Projekt beantworten lassen |

## Agent, Skill, Spec (siehe Lab 1.2)

| Konzept | Kurzbeschreibung                                                                         |
| ------- | ---------------------------------------------------------------------------------------- |
| Agent   | eigener Chatmodus (`.github/chatmodes/<name>.chatmode.md`) mit Rolle und erlaubten Tools |
| Skill   | Anleitung für wiederkehrende Aufgaben (`.github/skills/<name>/SKILL.md`)                 |
| Spec    | schriftliche Anforderungsbeschreibung vor der Codegenerierung (z. B. `SPEC.md`)          |

## Faustregeln

- Prompts konkret formulieren: was, womit, welches Format als Ergebnis.
- Von Copilot generierten Code immer lesen und verstehen, bevor er übernommen wird.
- Eine Spec schreiben, bevor eine komplexere KI-Aufgabe gestellt wird - das macht das Ergebnis überprüfbar.
