# Git-Cheatsheet

Schnellreferenz für die in Modul 2 (Grundlagen, lokales Repo, Commits/Historie) verwendeten Befehle.

## Repository einrichten

| Befehl                                     | Wirkung                                        |
| ------------------------------------------ | ---------------------------------------------- |
| `git init`                                 | neues, leeres Repo im aktuellen Ordner anlegen |
| `git clone <url>`                          | bestehendes Remote-Repo lokal kopieren         |
| `git config --global user.name "<name>"`   | globalen Commit-Autornamen setzen              |
| `git config --global user.email "<email>"` | globale Commit-E-Mail setzen                   |

## Änderungen verfolgen

| Befehl                         | Wirkung                                                         |
| ------------------------------ | --------------------------------------------------------------- |
| `git status`                   | Status von Arbeitsverzeichnis/Staging-Bereich anzeigen          |
| `git add <datei>`              | Datei zum Staging-Bereich hinzufügen                            |
| `git add .`                    | alle Änderungen im aktuellen Ordner stagen                      |
| `git diff`                     | ungestagte Änderungen anzeigen                                  |
| `git diff --staged`            | gestagte, aber noch nicht committete Änderungen anzeigen        |
| `git restore <datei>`          | Änderungen an einer Datei verwerfen                             |
| `git restore --staged <datei>` | Datei aus dem Staging-Bereich nehmen (Änderung bleibt erhalten) |

## Commits und Historie

| Befehl                      | Wirkung                                           |
| --------------------------- | ------------------------------------------------- |
| `git commit -m "<message>"` | gestagte Änderungen committen                     |
| `git log`                   | vollständige Commit-Historie anzeigen             |
| `git log --oneline`         | kompakte Ein-Zeilen-Historie                      |
| `git log --oneline --graph` | Historie inkl. Branch-/Merge-Struktur             |
| `git show <commit>`         | Details und Diff eines einzelnen Commits anzeigen |

## Branches (siehe auch Modul 3)

| Befehl                   | Wirkung                                    |
| ------------------------ | ------------------------------------------ |
| `git branch`             | lokale Branches auflisten                  |
| `git branch <name>`      | neuen Branch anlegen (ohne zu wechseln)    |
| `git checkout -b <name>` | Branch anlegen und direkt wechseln         |
| `git checkout <name>`    | zu bestehendem Branch wechseln             |
| `git merge <name>`       | angegebenen Branch in den aktuellen mergen |
| `git branch -d <name>`   | lokalen Branch löschen (nur wenn gemerged) |

## Remotes (siehe auch Modul 3)

| Befehl                        | Wirkung                                        |
| ----------------------------- | ---------------------------------------------- |
| `git remote add origin <url>` | Remote-Repo verknüpfen                         |
| `git remote -v`               | verknüpfte Remotes anzeigen                    |
| `git push -u origin main`     | Branch pushen und Tracking einrichten          |
| `git push`                    | Änderungen zum getrackten Remote-Branch pushen |
| `git pull`                    | Änderungen vom Remote-Branch holen und mergen  |

## Faustregeln

- Kleine, thematisch klare Commits statt großer Sammel-Commits.
- Vor `git push` immer `git status`/`git log` prüfen, was tatsächlich committet wird.
- `git restore`/`git reset` sind destruktiv - bei Unsicherheit zuerst `git status` und `git diff` prüfen.
