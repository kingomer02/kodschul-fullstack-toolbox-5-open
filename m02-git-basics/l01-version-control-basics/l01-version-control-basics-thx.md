# Modul 2: Einstieg in Versionskontrolle und Git

## Lab 2.1 - Warum Versionskontrolle? Grundbegriffe

---

## Lab-Ziel

Du kannst erklären, warum Versionskontrolle nötig ist, und kennst die Begriffe Repository, Commit und Diff.

**Leitfragen:**

<details>
<summary>Was passiert ohne Versionskontrolle bei parallelem Arbeiten an derselben Datei?</summary>

Änderungen überschreiben sich gegenseitig oder Teams behelfen sich mit Dateikopien wie `app_final_v2.js`, ohne nachvollziehbare Historie.

</details>

<details>
<summary>Was ist ein Commit, was ein Diff?</summary>

Ein Commit ist ein gespeicherter Schnappschuss von Änderungen mit Beschreibung; ein Diff zeigt die Differenz zwischen zwei Ständen.

</details>

<details>
<summary>Was speichert Git eigentlich - Dateien oder Änderungen?</summary>

Git speichert Schnappschüsse des gesamten Projektstands zu jedem Commit-Zeitpunkt, nicht einzelne Dateiversionen.

</details>

---

## Das Problem ohne Versionskontrolle

Ohne Versionskontrolle behelfen sich Teams oft mit Dateikopien wie `app_final_v2_wirklich.js`. Das führt zu:

- unklarer Herkunft von Änderungen ("wer hat das geändert, warum?"),
- keinem sicheren Weg zurück zu einem funktionierenden Stand,
- Konflikten, wenn zwei Personen gleichzeitig arbeiten.

**Versionskontrolle** macht jede Änderung nachvollziehbar, rückgängig machbar und teilbar.

---

## Grundbegriffe

| Begriff           | Bedeutung                                                            |
| ----------------- | -------------------------------------------------------------------- |
| Repository (Repo) | der versionierte Projektordner inkl. gesamter Historie               |
| Commit            | ein gespeicherter Schnappschuss von Änderungen mit Beschreibung      |
| Diff              | die Differenz zwischen zwei Ständen (was wurde hinzugefügt/entfernt) |
| Working Directory | deine aktuellen, noch nicht committeten Dateien                      |
| Staging Area      | Änderungen, die für den nächsten Commit vorgemerkt sind              |

Git speichert Schnappschüsse des gesamten Projektstands pro Commit, nicht einzelne Dateiversionen.

---

## Warum gerade Git?

Git ist dezentral: jede Repo-Kopie enthält die vollständige Historie, nicht nur ein zentraler Server.

- Das ermöglicht Arbeiten ohne Internetverbindung und ist die Grundlage für GitHub (Modul 3).

**Grenze:** Konventionen (z. B. Commit-Nachrichten, Branching-Strategie) entscheiden, ob die Historie später nützlich ist.

---

## Checkpoint

Du kannst in eigenen Worten den Unterschied zwischen Working Directory, Staging Area und Commit erklären.

Weiter geht es mit Lab 2.2: das erste lokale Repo für TeamBoard.
