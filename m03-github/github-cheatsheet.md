# GitHub-Cheatsheet

Schnellreferenz für die in Modul 3 (Repo pushen, Branching, Pull Requests) verwendeten Befehle und Konzepte.

## Repo verbinden und pushen

| Befehl                        | Wirkung                                        |
| ----------------------------- | ---------------------------------------------- |
| `git remote add origin <url>` | lokales Repo mit GitHub-Repo verknüpfen        |
| `git branch -M main`          | aktuellen Branch in `main` umbenennen          |
| `git push -u origin main`     | `main` erstmals pushen und Tracking einrichten |

## Authentifizierung

| Methode                       | Kurzbeschreibung                                                                   |
| ----------------------------- | ---------------------------------------------------------------------------------- |
| Personal Access Token (HTTPS) | in GitHub-Einstellungen erzeugen, statt Passwort beim Push verwenden               |
| SSH-Schlüssel                 | lokal erzeugen (`ssh-keygen`), öffentlichen Schlüssel im GitHub-Profil hinterlegen |

## Branching-Workflow

| Befehl                              | Wirkung                                  |
| ----------------------------------- | ---------------------------------------- |
| `git checkout -b feature/<name>`    | Feature-Branch anlegen und wechseln      |
| `git push -u origin feature/<name>` | Feature-Branch erstmals zu GitHub pushen |
| `git merge feature/<name>`          | Branch lokal in `main` mergen            |

## Merge-Konflikte

- Konfliktmarkierungen im Code: `<<<<<<<`, `=======`, `>>>>>>>`.
- Richtige Version wählen/kombinieren, Markierungen entfernen, dann `git add` + `git commit`.

## Pull Requests

| Schritt          | Wo                                                              |
| ---------------- | --------------------------------------------------------------- |
| PR erstellen     | GitHub: "Compare & pull request" nach Push eines Branches       |
| Review anfordern | Reviewer im PR zuweisen                                         |
| Mergen           | "Merge", "Squash and Merge" oder "Rebase and Merge" wählen      |
| Branch aufräumen | "Delete branch" auf GitHub, danach `git branch -d <name>` lokal |

## Merge-Strategien im Vergleich

| Strategie        | Effekt auf `main`-Historie                      |
| ---------------- | ----------------------------------------------- |
| Merge Commit     | alle Commits bleiben, zusätzlicher Merge-Commit |
| Squash and Merge | ein zusammengefasster Commit pro Feature        |
| Rebase and Merge | Branch-Commits linear vor `main` gesetzt        |

## Faustregeln

- Nie direkt Passwort statt Token/SSH-Schlüssel verwenden - GitHub akzeptiert das nicht mehr.
- PR-Beschreibung enthält: was, warum, wie testen.
- Nach dem Merge den Branch löschen, um das Repo übersichtlich zu halten.
