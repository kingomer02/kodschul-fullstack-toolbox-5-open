# Lab 1.2 - Übung: KI-gestützte Entwicklung mit Copilots

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - erzeugt den ersten TeamBoard-Entwurf.

## Ausgangslage

Copilot Chat ist in VS Code verfügbar und am GitHub-Konto angemeldet (Lab 1.1).

> **Korrektur (Durchlauf 09/2026, Ö. Akgeyik):** Copilot wird nicht mehr installiert - seit VS Code 1.138 ist es eingebaut. Es muss nur die Anmeldung am GitHub-Konto stehen.

## Aufgaben

1. Formuliere in Copilot Chat einen Prompt, der ein Markdown-Konzept für TeamBoard anfragt: Titel, Beschreibung, Zuständiger, Status (To Do/In Progress/Done), mögliche Aktionen (Ticket erstellen, zuweisen, Status ändern).
2. Lies den Vorschlag und identifiziere mindestens eine Stelle, die du korrigieren oder ergänzen willst (z. B. fehlende Statuswerte, falsche Aktionen).
3. Speichere den korrigierten Entwurf als `README-draft.md` in einem lokalen Ordner `teamboard/`.
4. Formuliere einen zweiten, gezielteren Prompt, der nur die Statuswerte als Aufzählung liefert, und vergleiche die Antwortqualität mit Aufgabe 1.
5. Schreibe zuerst eine kurze Spec (3-4 Stichpunkte: Ticket-Felder, Status-Werte, Aktionen) und formuliere danach den Prompt aus Aufgabe 1 erneut auf Basis dieser Spec. Halte in ein bis zwei Sätzen fest, ob der Vorschlag dadurch genauer wurde und ob die Aufgabe eher ein einzelner Prompt oder ein mehrschrittiger, agentischer Workflow war.

## Checkpoint

- `teamboard/README-draft.md` existiert und enthält alle vier genannten Ticket-Felder sowie die drei Status-Werte.
- Du kannst benennen, was du am ersten KI-Vorschlag korrigiert hast.
- Du kannst in ein bis zwei Sätzen den Unterschied zwischen Spec-first- und Prompt-ohne-Spec-Ergebnis benennen.

## Abschlusskriterien

- Datei liegt vor, Korrektur ist nachvollziehbar (z. B. per Kommentar oder kurzer Notiz im Dokument).

## Fallback

Ohne Copilot-Zugang: das gleiche Konzept manuell in Stichpunkten entwerfen und die Übung als Diskussion "was würde eine KI vorschlagen, was fehlt oft?" durchführen.
