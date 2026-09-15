# Modul 1: VS Code als Entwickler-Cockpit

## Lab 1.2 - KI-gestützte Entwicklung mit Copilots

---

## Lab-Ziel

Nach diesem Lab kannst du Copilot Chat gezielt für Erklärungen, Codevorschläge und einen ersten Projektentwurf einsetzen und kennst die Begriffe Prompt, Agent, Skill und Spec-driven Development.

**Leitfragen:**

<details>
<summary>Wofür ist Copilot Chat sinnvoll, wofür nicht?</summary>

Sinnvoll für Erklärungen, Boilerplate und erste Entwürfe; nicht sinnvoll als alleinige Quelle für sicherheitskritische oder fachlich unklare Entscheidungen.

</details>

<details>
<summary>Wie formulierst du einen Prompt, der einen brauchbaren, nachvollziehbaren Vorschlag liefert?</summary>

Ziel, erwarteten Umfang und konkrete Datenfelder/Constraints nennen, statt vage Formulierungen wie "Mach ein Ticket-System" zu verwenden.

</details>

<details>
<summary>Wie prüfst du einen KI-Vorschlag, bevor du ihn übernimmst?</summary>

Vorschlag gegen die eigenen Anforderungen lesen, fehlende oder falsche Teile identifizieren und vor der Übernahme manuell korrigieren.

</details>

<details>
<summary>Was unterscheidet einen Prompt von einem Agent und einem Skill?</summary>

Ein Prompt ist eine einzelne Anfrage, ein Agent führt mehrere Schritte selbstständig aus, ein Skill ist eine wiederverwendbare Anleitung, die der Agent bei Bedarf nachlädt.

</details>

---

## Agentische Workflows: Grundidee

Ein "agentischer" Workflow arbeitet über mehrere Schritte an einer Aufgabe statt nur eine Zeile zu vervollständigen:

- liest Dateien, macht Vorschläge, ändert Code, erklärt das Ergebnis,
- Copilot Chat in VS Code unterstützt das in Grenzen (z. B. Änderungen über mehrere Dateien).

**Wichtige Regel für den ganzen Kurs:** Ein KI-Vorschlag ist ein Entwurf, keine fertige Antwort - du bleibst verantwortlich für Korrektheit und Sicherheit.

---

## Bausteine moderner KI-Unterstützung: Prompt, Agent, Skill

- **Prompt**: eine einzelne, gezielte Anfrage an die KI (z. B. "erkläre diese Funktion").
- **Agent**: ein KI-Modus, der mehrere Schritte selbstständig ausführt (Dateien lesen, Code ändern, Befehle vorschlagen) statt nur zu antworten.
- **Skill**: eine wiederverwendbare, dokumentierte Anleitung, die ein Agent bei Bedarf nachlädt, statt dass du sie jedes Mal neu erklärst.

**Grenze:** je mehr Autonomie ein Agent hat, desto wichtiger wird die Kontrolle seines Ergebnisses vor der Übernahme.

---

## Spec-driven Development: Grundidee

- Erst die Anforderung (Spec) schriftlich festhalten - z. B. Datenfelder, Regeln, Beispiele.
- Dann den Agent gegen diese Spec arbeiten lassen, nicht gegen eine vage Idee.
- Für TeamBoard heißt das: Ticket-Felder und Status-Werte zuerst schriftlich festhalten, bevor Code generiert wird.

**Vorteil:** eine schriftliche Spec macht das KI-Ergebnis überprüfbar und wiederholbar.

---

## How-to: Agent, Skill und Spec anlegen

- **Agent anlegen**: eigene Chatmodus-Datei unter `.github/chatmodes/<name>.chatmode.md` mit Rolle, erlaubten Tools und Verhalten anlegen.
- **Skill anlegen**: Ordner `.github/skills/<name>/SKILL.md` mit YAML-Frontmatter (`name`, `description`) und Schritt-für-Schritt-Anleitung anlegen.
- **Spec anlegen**: kurze Markdown-Datei (z. B. `SPEC.md`) mit Anforderungen, Datenfeldern und Beispielen schreiben, bevor Code generiert wird.

**Konkretes Beispiel:** dieses Kurs-Repo nutzt genau dieses Muster unter `.github/skills/` - jede Skill-Datei dort folgt derselben Struktur.

**Verbreitete Werkzeuge für diese Muster:**

| Werkzeug                      | Wofür                                                                 |
| ----------------------------- | --------------------------------------------------------------------- |
| GitHub Copilot Chat (VS Code) | Prompts, Agents und Skills direkt im Editor                           |
| GitHub Spec Kit               | Open-Source-Vorlagen für Spec-driven Development                      |
| LangChain / LangGraph         | Frameworks für eigene, komplexere Agenten (Ausblick, kein Kursinhalt) |

---

## Guter vs. schwacher Prompt

| Schwach                  | Besser                                                                                                                                                                               |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| "Mach ein Ticket-System" | "Erstelle ein Markdown-Konzept für ein minimales Kanban-Ticket-System mit Titel, Beschreibung, Zuständigem und Status (To Do/In Progress/Done). Keine Implementierung, nur Konzept." |

Ein guter Prompt nennt:

- das Ziel,
- den erwarteten Umfang (hier: nur Konzept, kein Code),
- die konkreten Datenfelder.

---

## Demo: README-Entwurf per Copilot Chat

1. Copilot-Chat-Ansicht öffnen.
2. Prompt wie oben eingeben.
3. Ergebnis lesen: Passen die Felder? Fehlt etwas (z. B. Statuswerte)?
4. Ergebnis manuell nachbessern, bevor es committed wird.

**Grenze:** Copilot kennt euer TeamBoard-Konzept noch nicht.

- Der erste Vorschlag ist generisch und braucht eure Korrektur.

---

## Checkpoint

Du hast einen Copilot-Chat-Prompt formuliert, den Vorschlag kritisch gelesen und mindestens eine Korrektur daran vorgenommen.

Weiter geht es mit Modul 2: Einstieg in Versionskontrolle und Git.
