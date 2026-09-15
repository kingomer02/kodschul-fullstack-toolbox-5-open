# Modul 2: Einstieg in Versionskontrolle und Git

## Lab 2.3 - Erste Commits, Status und Historie einsehen

---

## Lab-Ziel

Du kannst den Zustand eines Repos und seine Historie souverän untersuchen, bevor du weiterarbeitest.

**Leitfragen:**

<details>
<summary>Wie unterscheidest du "noch nicht gestagte" von "gestagten" Änderungen?</summary>

`git status` zeigt beides getrennt an: "Changes to be committed" sind gestaged (per `git add` vorgemerkt), "Changes not staged for commit" sind bekannte Dateien mit noch nicht vorgemerkten Änderungen.

</details>

<details>
<summary>Wie liest du `git log` und `git diff` gezielt für einen bestimmten Commit?</summary>

Mit `git log --oneline` für die Übersicht, `git log -p -- <datei>` für die Änderungen einer Datei über die Zeit und `git show <commit-hash>` für die Details eines einzelnen Commits.

</details>

---

## `git status` als ständiger Reflex

`git status` zeigt drei Kategorien:

- **Untracked**: neue Dateien, die Git noch nicht kennt,
- **Staged**: für den nächsten Commit vorgemerkt (`git add`),
- **Modified**: bekannte Dateien mit nicht gestagten Änderungen.

**Praxis-Regel:** vor jedem Commit `git status` prüfen.

- Verhindert versehentliches Commiten unfertiger oder falscher Dateien.

---

## Historie gezielt lesen

```bash
git log --oneline          # kompakte Übersicht
git log -p -- index.html   # Änderungen einer bestimmten Datei über die Zeit
git show <commit-hash>     # Details zu einem einzelnen Commit
```

Diese Befehle beantworten "Wer hat wann was geändert?".

- Wichtig, sobald mehrere Personen (Modul 3: GitHub) am selben Repo arbeiten.

---

## Checkpoint

Du kannst für einen beliebigen Commit im TeamBoard-Repo Autor, Zeitpunkt und geänderte Zeilen anzeigen.

Weiter geht es mit Modul 3: Zusammenarbeit mit GitHub.
