# Lab 3.1 - Übung: Repository auf GitHub anlegen und Projekt pushen

**Dauer:** ca. 30 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - TeamBoard existiert danach auch auf GitHub.

## Ausgangslage

Ein lokales `teamboard/`-Repo mit mindestens einem Commit existiert (Modul 2).

## Aufgaben

1. Lege auf GitHub ein neues, **leeres** Repository namens `teamboard` an - ohne README, ohne Lizenz, ohne `.gitignore`. Wähle als Sichtbarkeit **`Public`**.
2. Verbinde dein lokales Repo als `origin` mit dem GitHub-Repo.
3. Pushe den `main`-Branch und prüfe im Browser, dass die Dateien und die Commit-Historie sichtbar sind.
4. Ladet euch gegenseitig als Collaborator ein: `Settings` → `Collaborators` → `Add people`, GitHub-Benutzername der anderen Person.
5. Notiere in 1-2 Sätzen, welche Authentifizierungsmethode (Token oder SSH) du verwendet hast.

> **Warum leer:** Legt GitHub ein README oder eine Lizenz an, hat das Repo dort einen eigenen ersten Commit. Der erste Push wird dann abgelehnt (`rejected - fetch first`), weil beide Seiten eine Historie ohne gemeinsamen Ursprung haben.
>
> **Warum öffentlich:** In Lab 3.3 reviewt die jeweils andere Person euren Pull Request. Auf ein privates Repo hat sie keinen Zugriff. Nebeneffekt: Für öffentliche Repositories ist GitHub Actions unbegrenzt kostenlos - das betrifft Modul 4. Öffentlich heißt allerdings auch: **keine echten Zugangsdaten in dieses Repo, auch nicht testweise.**
>
> **Warum trotzdem die Einladung:** Die Felder `Assignee` und `Reviewer` bieten nur Personen mit ausdrücklichem Zugriff an. Die Einladung nehmt ihr an, indem ihr das Repo der anderen Person aufruft - dort erscheint oben ein Balken `Accept invitation`. Gearbeitet wird trotzdem die ganze Woche **jeder in seinem eigenen** Repo.
>
> **Zum Token:** Das GitHub-Passwort funktioniert seit 2021 nicht mehr für `git push`. Erzeugt einen Personal Access Token unter `Settings` → `Developer settings` → `Personal access tokens` → `Tokens (classic)` und setzt **beide** Haken: **`repo`** und **`workflow`**. Ohne `workflow` wird der Push in Modul 4 abgelehnt, sobald eine Datei unter `.github/workflows/` liegt.

## Checkpoint

- Das Repo `teamboard` existiert auf GitHub und zeigt den lokalen Commit-Verlauf.
- `git remote -v` zeigt eine `origin`-URL.

## Abschlusskriterien

- Push war erfolgreich, keine Fehlermeldung im Terminal.
- Dateien auf GitHub entsprechen dem lokalen Stand.

## Fallback

Ohne eigenen GitHub-Account: gemeinsam im Repo der anderen Kursperson arbeiten (als Collaborator) und den eigenen Stand lokal weiterführen.
