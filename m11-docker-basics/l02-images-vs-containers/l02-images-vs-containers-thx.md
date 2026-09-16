# Modul 11: Docker-Grundlagen

## Lab 11.2 - Images vs. Container

---

## Lab-Ziel

Du kannst erklären, warum mehrere Container aus demselben Image unabhängig voneinander laufen, und Image-Varianten (Tags) unterscheiden.

**Leitfragen:**

<details>
<summary>Was ist ein Image, was ist ein Container?</summary>

Ein Image ist eine unveränderliche, schreibgeschützte Vorlage (Dateisystem-Schichten + Metadaten); ein Container ist eine laufende Instanz davon mit einer eigenen, beschreibbaren Schicht obenauf.

</details>

<details>
<summary>Warum ändert sich das Ausgangs-Image nicht, wenn ein Container Dateien schreibt?</summary>

Container schreiben in eine eigene, container-spezifische Schicht ("Copy-on-Write") - das darunterliegende Image bleibt für alle Container aus diesem Image unverändert.

</details>

<details>
<summary>Wofür steht ein Image-Tag wie `node:20-alpine`?</summary>

`node` ist das Repository/der Image-Name, `20-alpine` der Tag - hier: Node.js-Version 20 auf Basis des schlanken Alpine-Linux-Unterbaus.

</details>

---

## Ein Image, mehrere Container

```bash
docker run --name c1 -d nginx
docker run --name c2 -d nginx
```

- Beide Container nutzen dasselbe `nginx`-Image, laufen aber unabhängig: unterschiedliche IDs, unterschiedlicher Lebenszyklus.
- Änderungen in `c1` (z. B. eine Datei im Container erzeugen) sind in `c2` nicht sichtbar.

---

## Tags und Image-Größe vergleichen

```bash
docker pull node:20
docker pull node:20-alpine
docker images
```

| Tag              | Typische Größe (Richtwert) | Grund                                              |
| ---------------- | -------------------------- | -------------------------------------------------- |
| `node:20`        | groß (~1 GB)               | vollständiges Debian-Basis-Image mit vielen Tools  |
| `node:20-alpine` | klein (~150-200 MB)        | schlankes Alpine-Linux, nur das Nötigste enthalten |

**Grenze:** Alpine-Images verwenden `musl` statt `glibc` - in seltenen Fällen kann das bei nativen Node-Modulen zu Kompatibilitätsproblemen führen. Für TeamBoard ist das unkritisch.

---

## Checkpoint

`docker images` zeigt beide `node`-Tags mit deutlich unterschiedlicher Größe; zwei gleichzeitig laufende `nginx`-Container sind über `docker ps` mit unterschiedlichen IDs sichtbar.

Weiter geht es mit Lab 11.3: eine Node.js-App containerisieren.
