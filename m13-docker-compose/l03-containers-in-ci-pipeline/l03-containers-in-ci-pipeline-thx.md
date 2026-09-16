# Modul 13: Mehrere Services mit Docker Compose verbinden

## Lab 13.3 - Ausblick: Container in der CI-Pipeline

---

## Lab-Ziel

Du kannst die bestehende CI-Pipeline aus Modul 4 um einen Schritt ergänzen, der die Compose-Konfiguration selbst validiert, und verstehst, warum ein voller Compose-Start in CI mehr Aufwand bedeutet.

**Leitfragen:**

<details>
<summary>Was prüft `docker compose config`, und was prüft es nicht?</summary>

Es prüft, ob die YAML-Syntax und die Grundstruktur (Services, Variablen-Referenzen) gültig sind - es startet keine Container und prüft keine Laufzeit-Erreichbarkeit.

</details>

<details>
<summary>Warum ist ein voller `docker compose up` in der CI-Pipeline aufwendiger als lokal?</summary>

Der CI-Runner müsste zusätzlich Docker-in-Docker bzw. eine Docker-Umgebung bereitstellen, Wartezeiten für Healthchecks einplanen und die Umgebung nach jedem Lauf sauber wieder abbauen.

</details>

---

## `docker compose config` als CI-Schritt

```yaml
# .github/workflows/ci.yml (Ausschnitt, ergänzt)
- run: npm run lint
- run: npm run build
- run: docker compose config
```

- `docker compose config` gibt die aufgelöste, validierte Compose-Konfiguration aus (oder bricht bei einem Syntaxfehler ab) - ein schneller, risikoarmer Smoke-Test ohne echten Container-Start.

---

## Ausblick auf einen vollen Container-CI-Lauf

Ein vollständiger `docker compose up` inklusive Backend- und MongoDB-Start in der CI-Pipeline wäre möglich, würde aber zusätzlich benötigen:

- Wartelogik, bis MongoDB tatsächlich Verbindungen annimmt (nicht nur gestartet ist),
- eine definierte Aufräumroutine (`docker compose down -v`) am Ende jedes Laufs,
- ggf. längere Laufzeiten, die gegen die Kurszeitplanung (Modul 4: einfache Lint/Build-Pipeline) abgewogen werden müssen.

**Grenze:** Dieser Kurs führt nur die Konfigurationsprüfung (`docker compose config`) in CI ein - ein voller Container-Start in der Pipeline ist eine reale, aber hier nicht umgesetzte Erweiterung.

---

## Checkpoint

Der CI-Lauf auf GitHub zeigt einen zusätzlichen, grünen Schritt für `docker compose config`.

## Projektbezug

Damit ist die CI-Pipeline aus Modul 4 seit Modul 13 immer aktuell zur jeweiligen Compose-Konfiguration - Modul 14 baut auf dem Backend im Container die erste REST-API.
