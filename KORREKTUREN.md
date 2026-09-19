# Korrekturen an den Kursunterlagen

**Fork von** [`kodschul/kodschul-fullstack-toolbox-5-open`](https://github.com/kodschul/kodschul-fullstack-toolbox-5-open) · **Stand:** 19.09.2026 · **Bearbeitet von:** Ömer Akgeyik

Die Unterlagen wurden für den Durchlauf **webFDT, 21.–25.09.2026 (ETC Wien)** vollständig durchgearbeitet — jedes Lab ausgeführt, jeder Checkpoint geprüft, jede Zahl nachgemessen. Dabei sind 17 Stellen aufgefallen, die nicht funktionieren, sich widersprechen oder veraltet sind.

Jede Änderung steht an Ort und Stelle im Text, gekennzeichnet als **„Korrektur (Durchlauf 09/2026, Ö. Akgeyik)"**. Nichts wurde stillschweigend entfernt.

---

## Geändert im Material

| # | Wo | Was war das Problem | Was jetzt dasteht |
|---|---|---|---|
| 1 | **Lab 1.1 / 1.2**, `00-setup-and-installation.md` | Copilot soll über den Marketplace installiert werden. Seit VS Code 1.138 ist Copilot eingebaut, die Installation schlägt fehl | Anmeldung am GitHub-Konto statt Installation |
| 2 | **Lab 3.2** (Kopf) | „Ändert die TeamBoard-Projektbasis? **Nein** — nutzt ein Übungsrepo", während Aufgabe 4 den Merge im TeamBoard verlangt | auf **Ja** korrigiert, mit Hinweis auf die Folge für Lab 3.3 |
| 3 | **Lab 3.3** (Ausgangslage, Aufgaben) | Setzt `feature/setup` „aus Lab 2.2/2.3" voraus. Dort wird kein Branch angelegt, und aus Lab 3.2 ist er bereits gemergt — der PR wäre leer | neuer Branch `feature/readme`, vorheriger `git push origin main` als Aufgabe 0 |
| 4 | **Lab 3.3** (Inhalt des PR) | — | PR legt `README.md` an. Grund: Die Transfer-Übung Modul 4 trägt die CI-Badge in `README.md` ein, das es sonst nie gibt |
| 5 | **Lab 4.1** | „Lege **im Übungsrepo** …" — ein solches Repo wird im Kurs nirgends angelegt. Actions läuft zudem nur serverseitig, ein lokaler Ordner scheidet aus | TeamBoard-Repo, Branch `feature/ci-setup`. Dieselbe Datei wächst in Lab 4.2 zur echten Pipeline |
| 6 | **Lab 4.1** (Fallback) | — | Hinweis: Der Zugangstoken braucht **`workflow`** zusätzlich zu `repo`, sobald `.github/workflows/` gepusht wird |
| 7 | **Lab 4.2** | `npm init -y` erzeugt keine `package-lock.json`, `npm ci` bricht deshalb ab | `npm install --package-lock-only` ergänzt, mit der echten Fehlermeldung |
| 8 | **Transfer-Übung Modul 4** | Badge soll ins `README.md` — das im Originalablauf nicht existiert | Hinweis auf Lab 3.3, wo es jetzt entsteht |
| 9 | **Lab 6.1** | Erwartet „NaN". Gemessen: `discount(100, "10")` → **90**. Das Kernargument für TypeScript bricht damit live zusammen | `null` und `[]` als Fälle ergänzt — beide liefern **100**, plausibel und falsch, ohne Fehlermeldung |
| 10 | **Lab 6.2** | Skripte werden in `backend/package.json` ersetzt, die Pipeline läuft im Root — die CI bleibt grün, ohne je TypeScript kompiliert zu haben | `working-directory: backend` im Workflow ergänzt |
| 11 | **Lab 8.1** | `class Notification` kollidiert mit dem DOM-Typ: `TS2300: Duplicate identifier` | `"lib": ["ES2022"]` in der tsconfig, alternativ umbenennen |
| 12 | **Lab 13.2** | Checkpoint verlangt `backend` als `running`. Unerreichbar, weil `index.ts` kein Server ist — Lab 11.3 sagt das selbst | Checkpoint auf `Exited (0)` korrigiert, mit Überleitung auf Modul 14 |
| 13 | **Lab 14.2** | „die drei Beispieltickets aus Modul 7" — dort sind es zwei | Zahl entfernt, Hinweis auf die Inkonsistenz |
| 14 | **Lab 16.3** | Sichert nur `/tickets`. Gemessen: `GET /tickets` → `401`, `POST /graphql` → **`200` mit allen Daten** | Zusatzaufgabe ergänzt: `/graphql` ohne Token aufrufen und sehen, dass es offen ist |
| 15 | **Modul 15** | `apollo-server` / `apollo-server-express` sind seit 11/2023 abgekündigt | `@apollo/server` + `@as-integrations/express4` |
| 16 | **Module 4, 10–13** | Node 20 ist seit April 2026 End-of-Life, `actions/checkout@v4` ist drei Hauptversionen alt | Node 24 LTS, `checkout@v7`, `setup-node@v7`, MongoDB 8 |
| 17 | **Repo-Wurzel** | Kein README — wer den Link bekommt, landet in 22 Ordnern ohne Einstieg | `README.md` mit Aufbau, Setup-Liste und Wochenübersicht |

**Gemessene Werte**, die geschätzte Angaben ersetzt haben: `node:24` **1,64 GB** gegen `node:24-alpine` **238 MB** · Multi-Stage-Image **249 MB** gegen Single-Stage **293 MB**.

---

## Nicht geändert, aber erwähnenswert

**Der Donnerstag ist überbucht.** Die Module 14–17 summieren sich auf **445 Minuten Übung bei 345 Minuten Nettozeit**; allein Modul 17 verlangt 145 Minuten in einem 75-Minuten-Block. Das ist keine Fehlstelle im Text, sondern eine Frage der Zeitplanung — sie lässt sich nur durch Kürzen oder Verschieben lösen, nicht durch eine Korrektur im Material.

**`m00-overview/best-practices.md`** versprach, ein Wechsel auf MongoDB betreffe „nur das Repository, nicht den Service". Das ist abgeschwächt worden: `async` zieht sich durch alle aufrufenden Schichten.

---

## Herkunft

Das Original stammt von Kodschul und ist dort weiterhin maßgeblich. Dieser Fork existiert, damit die Teilnehmenden des Durchlaufs im September 2026 mit Unterlagen arbeiten, die durchlaufen — und damit die Funde an einer Stelle nachvollziehbar dokumentiert sind. Sie wurden dem Urheber zusätzlich als Pull Request angeboten.
