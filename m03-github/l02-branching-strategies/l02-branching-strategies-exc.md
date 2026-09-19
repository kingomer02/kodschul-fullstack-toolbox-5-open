# Lab 3.2 - Übung: Branching-Strategien im Team

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - der Branch `feature/setup` wird hier lokal in `main` gemerged.

> **Hinweis:** Der Merge findet bewusst im TeamBoard statt - einmal im Terminal zu sehen, wie ein Konflikt entsteht und aufgelöst wird, ist der Kern dieser Übung. Der Branch `feature/setup` ist danach aufgebraucht; Lab 3.3 legt deshalb einen neuen an.

## Ausgangslage

Ein GitHub-Repo mit gepushtem `main`-Branch existiert (Lab 3.1).

## Aufgaben

1. Lege lokal einen Branch `feature/setup` an.
2. Ändere im Branch eine Kleinigkeit (z. B. einen Kommentar in `index.html` oder `README.md`) und committe die Änderung.
3. Wechsle zurück auf `main` und ändere dort bewusst dieselbe Zeile anders, committe erneut.
4. Versuche `feature/setup` in `main` zu mergen, löse den entstehenden Konflikt und schließe den Merge ab.

## Checkpoint

- `git log --oneline --graph` zeigt beide Branches und den Merge-Commit.
- Der Konflikt wurde manuell aufgelöst, keine Konfliktmarkierungen (`<<<<<<<`) sind mehr im Code.

## Abschlusskriterien

- `main` enthält nach dem Merge eine bewusst gewählte, konfliktfreie Version der Zeile.

## Fallback

Ohne Konflikt-Erfahrung: den Trainer den Konflikt live erzeugen und auflösen lassen, danach denselben Ablauf an einer eigenen kleinen Änderung nachvollziehen.
