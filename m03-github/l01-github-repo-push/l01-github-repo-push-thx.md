# Modul 3: Zusammenarbeit mit GitHub

## Lab 3.1 - Repository auf GitHub anlegen und Projekt pushen

---

## Lab-Ziel

Du hast ein GitHub-Repository angelegt und dein lokales Repo dorthin gepusht.

**Leitfragen:**

<details>
<summary>Was ist der Unterschied zwischen Git und GitHub?</summary>

Git ist die Versionskontroll-Software; GitHub ist ein Hosting-Dienst dafür mit Zusammenarbeit, Issues, Actions und Pull Requests.

</details>

<details>
<summary>Was ist ein "Remote", und wie hängt er mit deinem lokalen Repo zusammen?</summary>

Ein Remote ist eine benannte Referenz auf ein entferntes Repo (z. B. `origin`); `git push`/`git pull` synchronisieren lokale und entfernte Historie darüber.

</details>

<details>
<summary>Warum HTTPS oder SSH für die Authentifizierung, statt Benutzername/Passwort?</summary>

GitHub akzeptiert seit 2021 kein Account-Passwort mehr für Git-Operationen - nötig sind ein Personal Access Token (HTTPS) oder ein SSH-Schlüssel.

</details>

---

## Git vs. GitHub

- **Git**: lokale Versionskontrolle, läuft ohne Internet.
- **GitHub**: Cloud-Hosting für Git-Repos plus Teamfunktionen (Pull Requests, Actions, Issues).

**Grenze:** ein lokales Repo braucht keinen GitHub-Account - GitHub wird erst für Zusammenarbeit und Backup nötig.

---

## Remote verbinden und pushen

```bash
git remote add origin <repo-url>
git branch -M main
git push -u origin main
```

- `git remote add origin` verknüpft das lokale Repo mit der GitHub-URL.
- `-u` merkt sich die Verknüpfung, sodass spätere `git push` ohne Zusatzangaben funktionieren.

---

## Authentifizierung

| Methode                       | Ablauf                                                                      |
| ----------------------------- | --------------------------------------------------------------------------- |
| HTTPS + Personal Access Token | Token in GitHub erzeugen, statt Passwort beim Push eingeben                 |
| SSH-Schlüssel                 | Schlüsselpaar erzeugen, öffentlichen Schlüssel im GitHub-Profil hinterlegen |

**Grenze:** Tokens/Schlüssel sind Zugangsdaten - niemals ins Repo committen.

---

## Checkpoint

Das TeamBoard-Repo ist auf GitHub sichtbar und enthält den bisherigen lokalen Commit-Verlauf.

Weiter geht es mit Lab 3.2: Branching-Strategien im Team.
