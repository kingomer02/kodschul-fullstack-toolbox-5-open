# Modul 1: VS Code als Entwickler-Cockpit

## Lab 1.1 - VS Code Konfiguration und Erweiterungen

---

## Lab-Ziel

Nach diesem Lab hast du VS Code kursweit einsatzbereit konfiguriert und kennst die Erweiterungen, die in den folgenden Modulen benutzt werden.

**Leitfragen:**

<details>
<summary>Welche VS-Code-Erweiterungen brauchst du für TypeScript, Docker und Git?</summary>

ESLint, Prettier, Docker und GitLens (plus GitHub Copilot/Copilot Chat für KI-Unterstützung).

</details>

<details>
<summary>Wie richtest du Workspace-Einstellungen ein, die für das ganze Team gelten?</summary>

Über eine `.vscode/settings.json` im Projektordner, damit die Einstellungen mit dem Repo geteilt werden statt im persönlichen User-Profil zu liegen.

</details>

<details>
<summary>Wie prüfst du, ob deine lokale Toolchain (Node.js, Git, Docker Desktop) läuft?</summary>

Im integrierten Terminal mit `node -v`, `git --version` und `docker --version` - jeder Befehl muss eine Versionsnummer statt einer Fehlermeldung liefern.

</details>

<details>
<summary>Welche Copilot-Einstellungen sind für den Datenschutz relevant?</summary>

"Copilot -> Enable/Disable" pro Sprache sowie die Einstellung, ob Codevorschläge aus öffentlichem Code ausgeschlossen werden (`github.copilot.advanced.contentExclusions` bzw. die Organisationsrichtlinie) - in Firmenumgebungen regelt das die IT/der Datenschutzbeauftragte, nicht jede einzelne Person.

</details>

---

## Warum VS Code als Cockpit?

VS Code bündelt Editor, Terminal, Git-Client, Docker-Integration und KI-Unterstützung in einem Fenster.

- Ein sauber konfiguriertes Setup spart wiederkehrende Reibung (fehlende Formatierung, falsche Node-Version, kein Docker-Zugriff).

**Wichtige Erweiterungen für diesen Kurs:**

| Erweiterung                   | Zweck                                         |
| ----------------------------- | --------------------------------------------- |
| ESLint                        | Code-Qualität für JavaScript/TypeScript       |
| Prettier                      | konsistente Formatierung                      |
| Docker                        | Container/Images direkt aus VS Code verwalten |
| GitLens                       | erweiterte Git-Historie und Blame-Ansicht     |
| GitHub Copilot / Copilot Chat | KI-gestützte Codevervollständigung und Chat   |

---

## Workspace-Einstellungen

Eine `.vscode/settings.json` im Projektordner sorgt dafür, dass alle Teilnehmer dieselben Grundeinstellungen nutzen, unabhängig vom persönlichen VS-Code-Profil:

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "files.eol": "\n"
}
```

**Grenze:** persönliche Einstellungen (Theme, Tastenkürzel) bleiben im User-Profil, nicht im Projekt-Workspace.

- Sonst überschreibt jeder Commit die Vorlieben der anderen.

---

## Copilot: Datenschutz und Ausschlüsse

- Firmen-/Kunden-Repos können per Content-Exclusion-Regel bestimmte Dateien/Ordner von Copilot-Vorschlägen ausschließen (z. B. Secrets-Ordner).
- Ob Codevorschläge auf Basis öffentlicher Trainingsdaten erlaubt sind, wird meist zentral über die GitHub-Organisation festgelegt, nicht lokal je Person.

**Für diesen Kurs:** die Standardeinstellungen genügen, da TeamBoard ein Übungsprojekt ohne echte Geheimnisse ist - im echten Projektalltag vorher mit IT/Datenschutz klären.

---

## Checkpoint

Du hast:

- [ ] die vier Kurs-Erweiterungen installiert (ESLint, Prettier, Docker, GitLens),
- [ ] `.vscode/settings.json` in einem Testordner angelegt,
- [ ] per Terminal in VS Code geprüft, dass `node -v`, `git --version` und `docker --version` funktionieren.

Weiter geht es mit Lab 1.2: Copilot Chat produktiv einsetzen.
