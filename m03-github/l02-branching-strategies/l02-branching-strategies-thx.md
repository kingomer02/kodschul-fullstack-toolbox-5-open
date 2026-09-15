# Modul 3: Zusammenarbeit mit GitHub

## Lab 3.2 - Branching-Strategien im Team

---

## Lab-Ziel

Du kannst einen Feature-Branch anlegen, isoliert daran arbeiten und ihn wieder mit `main` zusammenführen.

**Leitfragen:**

<details>
<summary>Warum nicht einfach direkt auf `main` arbeiten?</summary>

Direkte Änderungen auf `main` riskieren einen kaputten Hauptstand; ein Branch isoliert unfertige Arbeit, bis sie geprüft ist.

</details>

<details>
<summary>Was passiert bei einem Merge-Konflikt, und wie löst du ihn?</summary>

Git kann zwei sich überschneidende Änderungen nicht automatisch vereinen; die betroffenen Zeilen werden markiert und müssen manuell entschieden und committet werden.

</details>

<details>
<summary>Welche Branching-Strategie passt zu einem kleinen Team?</summary>

Ein einfacher Trunk-based-Ansatz (kurzlebige Feature-Branches, häufige Merges in `main`) statt komplexer Modelle wie Git Flow.

</details>

---

## Feature-Branch-Workflow

```bash
git checkout -b feature/ticket-form
# Änderungen vornehmen und committen
git checkout main
git merge feature/ticket-form
```

- `checkout -b` erstellt und wechselt in einem Schritt auf einen neuen Branch.
- `main` bleibt währenddessen unverändert und stabil.

---

## Branching-Strategien im Vergleich

| Strategie   | Merkmal                                               | Geeignet für                     |
| ----------- | ----------------------------------------------------- | -------------------------------- |
| Trunk-based | kurzlebige Branches, häufige Merges in `main`         | kleine Teams, schnelle Iteration |
| Git Flow    | feste Branches wie `develop`, `release/*`, `hotfix/*` | größere Teams, geplante Releases |

**Für diesen Kurs:** Trunk-based, weil TeamBoard von einem kleinen Team kontinuierlich weiterentwickelt wird.

---

## Merge-Konflikte

Ein Konflikt entsteht, wenn zwei Branches dieselbe Zeile unterschiedlich geändert haben.

- Git markiert die Stelle mit `<<<<<<<`, `=======`, `>>>>>>>`.
- Die richtige Version auswählen oder von Hand kombinieren, dann `git add` und `git commit`.

---

## Checkpoint

Ein Feature-Branch wurde erstellt, verändert und erfolgreich in `main` gemerged.

Weiter geht es mit Lab 3.3: Pull Requests erstellen, reviewen und mergen.
