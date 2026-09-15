# Modul 2: Einstieg in Versionskontrolle und Git

## Lab 2.2 - Lokales Repo für das Kursprojekt anlegen

---

## Lab-Ziel

Du hast ein lokales Git-Repository für TeamBoard angelegt und das erste HTML-Grundgerüst committet.

**Leitfragen:**

<details>
<summary>Welche Dateien gehören in den ersten Commit, welche nicht (z. B. `node_modules/`)?</summary>

In den ersten Commit gehören die eigenen Quelldateien (z. B. das HTML-Grundgerüst); generierte oder sensible Dateien wie `node_modules/`, `dist/` oder `.env` nicht.

</details>

<details>
<summary>Wie verhindert `.gitignore`, dass unerwünschte Dateien versioniert werden?</summary>

`.gitignore` listet Datei- und Ordnermuster, die Git beim Tracking ignoriert - diese Dateien tauchen dann nicht mehr unter "Untracked" bei `git status` auf und werden nie versioniert.

</details>

---

## Von der Einzelübung zum Projekt

Lab 2.1 hat die Grundbegriffe an einer Wegwerf-Übung gezeigt. Jetzt wenden wir dieselben Schritte auf TeamBoard an.

**Wichtig:** ab jetzt ist jeder Commit Teil der TeamBoard-Historie - committe bewusst und mit aussagekräftigen Nachrichten.

---

## `.gitignore` von Anfang an

Auch wenn `node_modules/` erst in Modul 5 entsteht, lohnt sich eine `.gitignore` von Beginn an:

```gitignore
node_modules/
dist/
.env
```

**Grund:** generierte oder sensible Dateien gehören nicht in die Historie.

- Sie lassen sich jederzeit neu erzeugen bzw. dürfen nicht öffentlich werden.

---

## Checkpoint

Ein lokales `teamboard/`-Repo existiert mit einem ersten Commit, der ein einfaches HTML-Grundgerüst enthält, sowie einer `.gitignore`.

Weiter geht es mit Lab 2.3: Commits und Historie vertiefen.
