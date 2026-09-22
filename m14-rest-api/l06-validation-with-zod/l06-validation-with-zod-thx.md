# Modul 14: REST-APIs mit Express

## Lab 14.6 - Vertiefung: Eingaben validieren mit zod

---

## Lab-Ziel

TypeScript prüft nur, was der **Compiler** sieht. Was zur Laufzeit per HTTP hereinkommt, ist `any` - `req.body.title` kann eine Zahl sein, ein leerer String oder fehlen. Du prüfst Eingaben am Rand der Anwendung mit einem Schema und bekommst daraus gleichzeitig den TypeScript-Typ.

**Leitfragen:**

<details>
<summary>Warum hilft das `Ticket`-Interface hier nicht?</summary>

Interfaces existieren nur beim Kompilieren und sind im erzeugten JavaScript verschwunden (Modul 7). Zur Laufzeit gibt es nichts, womit man prüfen könnte. Ein Schema ist dagegen ein **Objekt**, das zur Laufzeit existiert und prüfen kann.

</details>

<details>
<summary>`400` oder `422`?</summary>

Verbreitete Konvention: `400 Bad Request`, wenn die Anfrage gar nicht lesbar ist (kaputtes JSON). `422 Unprocessable Content`, wenn sie lesbar ist, aber inhaltlich nicht passt (Titel fehlt, falscher Typ). Beides ist vertretbar - entscheidend ist, dass die API es **einheitlich** macht.

</details>

---

## zod in fünf Zeilen

```ts
import { z } from "zod";

const schema = z.strictObject({
  title: z.string().trim().min(1),
  assignee: z.string().default(""),
});

type Input = z.infer<typeof schema>;         // { title: string; assignee: string }

const result = schema.safeParse(req.body);   // wirft nicht, liefert success/error
if (result.success) result.data.title;       // geprüft UND typisiert
```

- `z.strictObject` lehnt **unbekannte** Felder ab. `z.object` würde sie stillschweigend entfernen.
- `.trim()` verändert den Wert: `"  Tests  "` wird zu `"Tests"`.
- `.default("")` setzt den Wert, wenn das Feld fehlt.
- `.partial()` macht alle Felder optional - gut für `PATCH`.
- `z.infer` erzeugt den TypeScript-Typ aus dem Schema: **eine** Quelle statt Interface und Prüfcode nebeneinander.

> ⚠️ **Stolperfalle:** `.partial()` behält `.default()`-Werte. Ein Update-Schema, das per `.partial()` aus dem Anlege-Schema entsteht, setzt bei jedem `PATCH` alle Felder mit Default wieder auf ihren Default - still und ohne Fehlermeldung.

---

## Brücke zu dem, was du kennst

zod entspricht Bean Validation (`@NotBlank`, `@Size`) in Java oder Pydantic in Python. Der Unterschied: Das Schema ist normaler Code, keine Annotation - und der Typ wird **aus** dem Schema abgeleitet, nicht umgekehrt. Pydantic macht es genauso.

---

## Checkpoint

Falsche Eingaben liefern `422` mit einer Liste, **welches** Feld **warum** falsch ist. Gültige Eingaben kommen bereinigt an (getrimmt, Defaults gesetzt).

## Projektbezug

Die Prüfung sitzt in den Routen, Repository und Service bekommen nur noch geprüfte Daten. In Lab 14.7 prüft dasselbe Werkzeug die Query-Parameter.
