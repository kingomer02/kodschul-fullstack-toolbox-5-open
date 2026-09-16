# TeamBoard: Setup & Installation

Zentrale Checkliste für alles, was vor bzw. während Modul 1-10 installiert und verifiziert sein muss. Trainer prüfen dies vor Kursbeginn (siehe `02-plan.md`, Abschnitt "Environment and Trainer Preparation"); Teilnehmende führen die Verifikationsbefehle in Lab 1.1 (VS Code) und Lab 10.1 (Docker) selbst noch einmal aus.

## Vor Kursbeginn zu installieren

| Werkzeug                | Empfohlene Version       | Verifikationsbefehl         | Gebraucht ab |
| ----------------------- | ------------------------ | --------------------------- | ------------ |
| VS Code                 | aktuelle stabile Version | `code --version`            | Modul 1      |
| Git                     | aktuelle stabile Version | `git --version`             | Modul 2      |
| Node.js (LTS)           | 20.x LTS                 | `node --version`            | Modul 5      |
| npm (kommt mit Node.js) | 10.x                     | `npm --version`             | Modul 5      |
| Docker Desktop          | aktuelle stabile Version | `docker --version`          | Modul 10     |
| GitHub-Account          | -                        | Login auf github.com prüfen | Modul 3      |

**Nur unter Windows zusätzlich:**

| Werkzeug | Zweck                  | Verifikationsbefehl |
| -------- | ---------------------- | ------------------- |
| WSL 2    | Docker-Desktop-Backend | `wsl --status`      |

## VS Code-Erweiterungen

Installation über die Extensions-Ansicht (`Cmd+Shift+X` / `Ctrl+Shift+X`) oder Kommandozeile:

```bash
code --install-extension dbaeumer.vscode-eslint
code --install-extension esbenp.prettier-vscode
code --install-extension ms-azuretools.vscode-docker
code --install-extension eamodio.gitlens
code --install-extension GitHub.copilot
code --install-extension GitHub.copilot-chat
```

| Erweiterung                   | Gebraucht ab |
| ----------------------------- | ------------ |
| ESLint                        | Modul 6      |
| Prettier                      | Modul 1      |
| Docker                        | Modul 10     |
| GitLens                       | Modul 2      |
| GitHub Copilot / Copilot Chat | Modul 1      |

## Vollständigkeits-Check (vor Modul 1)

```bash
code --version
git --version
node --version
npm --version
docker --version
```

Alle fünf Befehle müssen eine Versionsnummer liefern, keine Fehlermeldung ("command not found").

## Modulweise Installations-/Account-Bedarf

| Modul                     | Neu benötigt                                                                      |
| ------------------------- | --------------------------------------------------------------------------------- |
| 1 - VS Code/Copilot       | VS Code, GitHub-Copilot-Lizenz/Zugang                                             |
| 2 - Git-Grundlagen        | Git                                                                               |
| 3 - GitHub                | GitHub-Account, Personal Access Token oder SSH-Schlüssel                          |
| 4 - CI/CD (Actions)       | keine zusätzliche Installation (GitHub Actions läuft in der Cloud)                |
| 5 - Node.js               | Node.js, npm                                                                      |
| 6 - TypeScript-Intro      | keine zusätzliche Installation (`typescript` wird per npm im Projekt installiert) |
| 7 - TypeScript-Grundlagen | keine zusätzliche Installation                                                    |
| 8 - TypeScript-OOP        | keine zusätzliche Installation                                                    |
| 9 - JS/TS-Puffer          | keine zusätzliche Installation                                                    |
| 10 - Container-Intro      | Docker Desktop, unter Windows zusätzlich WSL 2                                    |

## Fallback bei Installationsproblemen

- Node.js/npm: vom Trainer bereitgestellten npm-Cache/Mirror oder eine Cloud-IDE (z. B. Codespace) nutzen.
- Docker Desktop: Referenz-Umgebung des Trainers oder Cloud-Terminal mit vorinstalliertem Docker nutzen, lokales Setup parallel zur Pause reparieren.
- GitHub-Account: Trainer stellt ein Übungsrepo zum Forken bereit, falls kein eigener Account rechtzeitig verfügbar ist.
