# Modul 12: Dockerfiles schreiben und optimieren

## Lab 12.3 - Image-Größe und Layer-Caching

---

## Lab-Ziel

Du kannst die Größe zweier Image-Varianten vergleichen und beobachten, welche Dockerfile-Schichten bei einem erneuten Build aus dem Cache stammen.

**Leitfragen:**

<details>
<summary>Woran erkennst du im Build-Log, dass eine Schicht aus dem Cache kommt?</summary>

An der Meldung `CACHED` (bzw. `Using cache` bei älteren Docker-Versionen) vor der jeweiligen Anweisung im Build-Output.

</details>

<details>
<summary>Warum wird eine Schicht neu gebaut, wenn sich vorher nichts an dieser Zeile geändert hat?</summary>

Weil Docker Schichten sequenziell cached: ändert sich eine frühere Anweisung (z. B. eine kopierte Datei), verfällt der Cache für alle nachfolgenden Schichten, auch wenn diese selbst unverändert sind.

</details>

<details>
<summary>Warum liefert `docker history` mehr Information als `docker images`?</summary>

`docker images` zeigt nur die Gesamtgröße; `docker history` schlüsselt sie pro Schicht auf und zeigt, welche Anweisung wie viel Platz braucht.

</details>

---

## Größe vergleichen

```bash
docker images | grep teamboard-backend
```

| Tag                     | Erwartete Tendenz                                   |
| ----------------------- | --------------------------------------------------- |
| Single-Stage (Modul 11) | größer - enthält `devDependencies` wie `typescript` |
| Multi-Stage (Modul 12)  | kleiner - nur Produktionsabhängigkeiten + `dist/`   |

```bash
docker history teamboard-backend:multistage
```

Zeigt jede Schicht mit ihrer jeweiligen Größe - hilfreich, um die teuerste Anweisung zu identifizieren.

---

## Cache-Verhalten beobachten

1. Baue das Image ein zweites Mal, **ohne** Codeänderung: `docker build -t teamboard-backend:multistage backend/`. Die meisten Schichten zeigen `CACHED`.
2. Ändere nur `backend/src/index.ts` (nicht `package.json`) und baue erneut: nur die Schichten ab `COPY . .` (Builder-Stage) werden neu gebaut, die `npm ci`-Schicht bleibt gecached.
3. Ändere stattdessen `backend/package.json` (z. B. eine neue Dev-Abhängigkeit) und baue erneut: jetzt wird auch `npm ci` neu ausgeführt, da sich die kopierte Datei geändert hat.

**Grenze:** Cache-Verhalten hängt von der Reihenfolge der Dockerfile-Anweisungen ab - deshalb liegt `COPY package.json package-lock.json ./` bewusst vor `COPY . .`.

---

## Checkpoint

`docker history` zeigt die Schichtgrößen des Multi-Stage-Images; ein Rebuild nach einer reinen Quellcodeänderung nutzt weiterhin den `npm ci`-Cache.

## Projektbezug

Der Multi-Stage-Build ist ab jetzt die Grundlage für alle weiteren Docker-Module - Modul 13 verbindet dieses Image per Docker Compose mit MongoDB.
