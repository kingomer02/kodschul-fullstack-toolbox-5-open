# Modul 3: Zusammenarbeit mit GitHub

## Lab 3.3 - Pull Requests erstellen, reviewen und mergen

---

## Lab-Ziel

Du kannst einen Pull Request erstellen, ihn nachvollziehbar beschreiben und über GitHub mergen.

**Leitfragen:**

<details>
<summary>Was ist ein Pull Request, und wozu dient er?</summary>

Ein Pull Request schlägt vor, einen Branch in einen anderen (meist `main`) zu übernehmen, und bietet dabei Review und Diskussion vor dem Merge.

</details>

<details>
<summary>Was gehört in eine gute PR-Beschreibung?</summary>

Was geändert wurde, warum, und wie man es testet - genug Kontext, damit eine zweite Person ohne Rückfrage reviewen kann.

</details>

<details>
<summary>Welche Merge-Strategien bietet GitHub an?</summary>

Merge Commit, Squash and Merge, Rebase and Merge - sie unterscheiden sich darin, wie die Historie nach dem Merge aussieht.

</details>

---

## Pull Request vs. direkter Merge

- Ein direkter `git merge` lokal braucht kein Review.
- Ein Pull Request auf GitHub macht die Änderung sichtbar, kommentierbar und (optional) an Checks gebunden, bevor sie in `main` landet.

**Für TeamBoard:** auch bei zwei Personen lohnt sich der PR-Workflow, um den Ablauf für spätere, größere Teams einzuüben.

---

## Einen PR erstellen

1. Branch pushen: `git push -u origin feature/setup`.
2. Auf GitHub: "Compare & pull request" auswählen.
3. Titel und Beschreibung ausfüllen (was, warum, wie testen).
4. Reviewer zuweisen (hier: die zweite Kursperson oder der Trainer).

---

## Review und Merge

| Merge-Strategie  | Effekt auf die Historie                                         |
| ---------------- | --------------------------------------------------------------- |
| Merge Commit     | behält alle Commits, fügt einen zusätzlichen Merge-Commit hinzu |
| Squash and Merge | fasst alle Commits des Branches zu einem zusammen               |
| Rebase and Merge | setzt die Branch-Commits linear vor `main`                      |

**Für diesen Kurs:** Squash and Merge, damit die `main`-Historie pro Feature genau einen aussagekräftigen Commit zeigt.

---

## Checkpoint

Ein Pull Request für `feature/setup` wurde erstellt, beschrieben und über GitHub gemerged; der Branch ist auf GitHub gelöscht.

Weiter geht es mit Modul 4: Continuous Integration mit GitHub Actions.
