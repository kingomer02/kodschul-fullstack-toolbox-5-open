# Modul 14: REST-APIs mit Express

## Lab 14.5 - Vertiefung: Router und zentrale Fehlerbehandlung

---

## Lab-Ziel

Bisher entscheidet jede Route selbst, wie ein Fehler aussieht. Und wo keine Route greift, antwortet Express mit einer HTML-Seite - bei kaputtem JSON sogar mit einem kompletten Stacktrace samt Dateipfaden. Du ziehst die Fehlerbehandlung an **eine** Stelle und lagerst die Ticket-Routen in einen eigenen Router aus.

**Leitfragen:**

<details>
<summary>Was sieht ein Client heute, wenn er kaputtes JSON schickt?</summary>

Status `400` - und als Body eine HTML-Seite mit dem Stacktrace: `SyntaxError: Expected double-quoted property name ... at JSON.parse ... at parse (/app/node_modules/body-parser/...)`. Der Server verrät damit Framework, Bibliotheken und Verzeichnisstruktur. Ein API-Client kann mit HTML ohnehin nichts anfangen.

</details>

<details>
<summary>Woran erkennt Express eine Fehler-Middleware?</summary>

An der **Anzahl der Parameter**: `(err, req, res, next)` - vier statt drei. Express ruft sie auf, sobald eine Route einen Fehler wirft oder `next(err)` aufruft. Sie muss **nach** allen Routen registriert werden.

</details>

---

## Die drei Bausteine

**1. Eine eigene Fehlerklasse** trägt den HTTP-Status mit:

```ts
export class HttpError extends Error {
  constructor(public readonly status: number, message: string, public readonly details?: unknown) {
    super(message);
  }
}
```

Routen **werfen** dann nur noch (`throw new HttpError(404, "ticket not found")`), statt die Antwort selbst zu bauen.

**2. Ein Fallback für unbekannte Routen** - eine normale Middleware mit drei Parametern, **nach** allen Routen.

**3. Die Fehler-Middleware** mit vier Parametern, ganz am Ende. Sie unterscheidet drei Fälle:
- eigener `HttpError` → dessen Status und Meldung
- kaputter JSON-Body → Express markiert den Fehler mit `err.type === "entity.parse.failed"` → `400`
- alles andere → `500` mit neutraler Meldung, Details **nur ins Log**

---

## Router

```ts
import { Router } from "express";
const router = Router();
router.get("/", ...);      // wird zu GET /tickets
router.get("/:id", ...);   // wird zu GET /tickets/:id
app.use("/tickets", router);
```

Ein Router ist eine Mini-App mit eigenen Routen, die unter einem Präfix eingehängt wird. Lab 16.2 nutzt dasselbe Muster für `/auth`.

---

## Brücke zu dem, was du kennst

Spring: `@RestControllerAdvice` mit `@ExceptionHandler`, eigene Exceptions mit `@ResponseStatus`. FastAPI: `HTTPException` und `@app.exception_handler`. Der Router entspricht einem `@RestController` mit `@RequestMapping("/tickets")`.

---

## Checkpoint

Kaputtes JSON → `400` mit JSON-Body, unbekannte Route → `404` mit JSON-Body, ein unerwarteter Fehler → `500` ohne Stacktrace beim Client, aber mit Stacktrace im Server-Log.

## Projektbezug

Ab Lab 14.6 wirft die Validierung einen `HttpError` mit Details - die Fehler-Middleware muss dafür nicht mehr angefasst werden.
