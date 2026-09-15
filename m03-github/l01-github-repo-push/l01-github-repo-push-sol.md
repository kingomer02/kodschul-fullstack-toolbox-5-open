# Lab 3.1 - Lösung: Repository auf GitHub anlegen und Projekt pushen

## Aufgabe 1-2: Repo anlegen und verbinden

```bash
git remote add origin https://github.com/<user>/teamboard.git
git branch -M main
```

Ein leeres Remote-Repo verhindert, dass GitHub bereits einen ersten Commit (z. B. README) anlegt, der dem lokalen Verlauf widerspricht.

## Aufgabe 3: Pushen und prüfen

```bash
git push -u origin main
```

Auf der GitHub-Repo-Seite erscheinen danach dieselben Dateien und Commits wie lokal (`git log --oneline`).

## Aufgabe 4: Authentifizierungsmethode

Beispielnotiz: "HTTPS mit Personal Access Token, in den Git-Credential-Manager gespeichert" oder "SSH-Schlüssel, im GitHub-Profil unter SSH Keys hinterlegt".

## Grenzen

Dieses Lab verbindet nur ein einzelnes lokales Repo mit GitHub - Teamarbeit mit mehreren Personen am selben Repo folgt in Lab 3.2 und 3.3.
