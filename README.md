# Fullstack Developer Toolbox: Technologien für die Webentwicklung

Kursunterlagen zum Training **webFDT** (5 Tage).

Über die Woche entsteht **TeamBoard**, ein Kanban-Ticketsystem: versioniert mit Git
und GitHub, geprüft durch eine CI-Pipeline, containerisiert mit Docker und Compose,
mit REST- und GraphQL-API über MongoDB, abgesichert per JWT und bedient über eine
React-Oberfläche.

## So arbeitest du mit diesen Unterlagen

Jedes Modul liegt in einem eigenen Ordner (`m01-…` bis `m22-…`). Darin findest du
pro Lab drei Dateien:

| Endung | Inhalt |
|---|---|
| `-thx.md` | Theorie — lies das zuerst |
| `-exc.md` | Übung — bearbeite sie selbstständig |
| `-sol.md` | Lösung — erst danach öffnen |

**Empfehlung:** Die Lösung erst aufschlagen, wenn du die Übung versucht hast. Der
Lerneffekt entsteht beim eigenen Versuch, nicht beim Lesen.

Zusätzlich liegen in mehreren Modulen **Cheatsheets** (z. B.
`m02-git-basics/git-cheatsheet.md`) — als Nachschlagewerk gedacht, auch über den
Kurs hinaus.

## Vor Kursbeginn installieren

| Werkzeug | Version | Prüfbefehl |
|---|---|---|
| VS Code | aktuell | `code --version` |
| Git | aktuell | `git --version` |
| Node.js | aktuelles LTS | `node --version` |
| npm | kommt mit Node.js | `npm --version` |
| Docker Desktop | aktuell | `docker --version` |
| GitHub-Account | – | Login auf github.com |

Unter Windows zusätzlich **WSL 2** als Backend für Docker Desktop (`wsl --status`).

VS-Code-Erweiterungen: ESLint, Prettier, Docker, GitLens.

> **GitHub Copilot:** In aktuellen VS-Code-Versionen ist Copilot bereits eingebaut.
> Eine Installation über den Marketplace schlägt fehl. Es genügt, sich in VS Code
> mit dem GitHub-Konto anzumelden.

Alle Details: [`00-setup-and-installation.md`](00-setup-and-installation.md)

## Überblick

| Datei | Inhalt |
|---|---|
| [`m00-overview/overview.md`](m00-overview/overview.md) | Kursziel, Zielgruppe, vollständige Agenda |
| [`m00-overview/topics.md`](m00-overview/topics.md) | alle Module und Labs auf einen Blick |
| [`m00-overview/faq.md`](m00-overview/faq.md) | häufige Fragen zum Ablauf |
| [`m00-overview/best-practices.md`](m00-overview/best-practices.md) | modulübergreifende Praktiken mit Begründung |
| [`m00-overview/glossary.md`](m00-overview/glossary.md) | Begriffe |
| [`project/README.md`](project/README.md) | das Kursprojekt TeamBoard |

## Die fünf Tage

| Tag | Module | Thema |
|---|---|---|
| 1 | 1–4 | VS Code, Git, GitHub, CI/CD |
| 2 | 5–9 | Node.js, TypeScript, OOP |
| 3 | 10–13 | Container, Docker, Compose |
| 4 | 14–17 | REST, GraphQL, MongoDB, Auth, Responsive UI |
| 5 | 18–22 | React, Angular im Vergleich, Cloud-Deployment |

---

## Hinweis zu dieser Fassung

Dies ist ein **Fork** von [`kodschul/kodschul-fullstack-toolbox-5-open`](https://github.com/kodschul/kodschul-fullstack-toolbox-5-open).
Das Original stammt von Kodschul. Für den Durchlauf **21.–25.09.2026 (webFDT, ETC Wien)** wurden
Stellen korrigiert, die beim vollständigen Durcharbeiten nicht funktioniert haben oder sich
widersprachen — veraltete Versionen, Übungen mit unerreichbaren Checkpoints und Labs, die Dateien
voraussetzen, die vorher nie entstehen.

Jede Änderung ist im Text als `**Korrektur (Durchlauf 09/2026, Ö. Akgeyik):**` gekennzeichnet.
Die vollständige Liste steht in [`KORREKTUREN.md`](KORREKTUREN.md).
