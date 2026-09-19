# Lab 3.3 - Übung: Pull Requests erstellen, reviewen und mergen

**Dauer:** ca. 35 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - der `feature/setup`-Branch wird final in TeamBoards `main` gemerged.

## Ausgangslage

Das TeamBoard-Repo liegt auf GitHub (Lab 3.1), der Konflikt-Merge aus Lab 3.2 ist lokal abgeschlossen.

> **Korrektur (Durchlauf 09/2026, Ö. Akgeyik):** Im Original stand hier: „Ein lokaler Branch `feature/setup` … existiert (z. B. aus Lab 2.2/2.3) und ist noch nicht auf GitHub.“ Beides trifft nicht zu: In Lab 2.2/2.3 wird kein Branch angelegt (alles läuft auf `main`), und `feature/setup` aus Lab 3.2 ist bereits gemergt - ein Pull Request daraus wäre leer. Die Aufgaben unten legen deshalb einen **neuen** Branch an.

## Aufgaben

0. **Zuerst `git push origin main`** - die Commits aus Lab 3.2 liegen bisher nur lokal. Ohne diesen Schritt erscheinen sie später mit im Pull Request, weil ein PR immer gegen den Stand auf GitHub vergleicht.
1. Lege einen neuen Branch an: `git checkout -b feature/readme`. Erstelle darin ein **`README.md`** (acht Zeilen genügen: was TeamBoard ist, die Statuswerte, ein Abschnitt „Stand“ mit dem, was heute schon läuft), committe es und pushe den Branch.
2. Erstelle daraus einen Pull Request mit Titel und einer 2-3-sätzigen Beschreibung (was, warum, wie testen).

> **Korrektur (Durchlauf 09/2026, Ö. Akgeyik):** Warum ausgerechnet ein `README.md`: Das Projekt hat bisher nur `README-draft.md`, den Konzeptentwurf aus Modul 1. Die **Transfer-Übung in Modul 4 trägt die CI-Badge in `README.md` ein** - eine Datei, die es im Originalablauf zu dem Zeitpunkt gar nicht gibt. Hier entsteht sie.
3. Lasse den PR reviewen (durch die zweite Kursperson oder den Trainer) und ergänze mindestens einen Kommentar oder eine Korrektur.
4. Merge den PR mit "Squash and Merge" und lösche den Branch auf GitHub.

## Checkpoint

- Der PR ist auf GitHub als "Merged" markiert.
- `main` enthält die Änderung als einen einzigen, aussagekräftigen Commit.
- `README.md` liegt auf `main` (Voraussetzung für die Transfer-Übung in Modul 4).

## Abschlusskriterien

- PR-Beschreibung ist ohne Rückfrage verständlich.
- Branch ist nach dem Merge gelöscht (lokal und/oder auf GitHub).

## Fallback

Ohne zweite Reviewer-Person: der Trainer übernimmt das Review; die Teilnehmerin reviewt im Gegenzug einen vorbereiteten Trainer-PR.
