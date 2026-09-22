# Lab 14.7 - Lösung: Filtern, Sortieren, Paginieren

## Aufgabe 1-2: Entwurf

| Parameter | Werte | Bedeutung |
|---|---|---|
| `status` | `To Do`, `In Progress`, `Done` | nur Tickets mit diesem Status |
| `assignee` | Text | nur Tickets dieser Person |
| `sort` | `title`, `assignee` | Sortierfeld |
| `order` | `asc` (Standard), `desc` | Richtung |
| `limit` | 1-100 | Seitengröße, ohne Angabe: alle |
| `offset` | ab 0 | wie viele Treffer übersprungen werden |

**Gesamtzahl per Header `X-Total-Count`**, der Body bleibt ein Array. Das React-Frontend am Freitag und alle `curl`-Aufrufe aus den Transfer-Übungen erwarten ein Array - ein Umschlag-Objekt würde sie brechen.

## Aufgabe 3: Schema

```ts
// backend/src/validation/ticket-schemas.ts (Ergänzung)
// Query-Parameter kommen immer als Text an - coerce wandelt "10" in 10 um
export const listQuerySchema = z.strictObject({
  status: z.enum(["To Do", "In Progress", "Done"]).optional(),
  assignee: z.string().min(1).optional(),
  sort: z.enum(["title", "assignee"]).optional(),
  order: z.enum(["asc", "desc"]).optional(),
  limit: z.coerce.number().int().min(1).max(100).optional(),
  offset: z.coerce.number().int().min(0).optional(),
});
```

## Aufgabe 4: Repository

```ts
// backend/src/repositories/ticket-repository.ts
import { Ticket } from "../models/ticket";
import { Repository } from "./repository";

export interface TicketQuery {
  status?: Ticket["status"];
  assignee?: string;
  sort?: "title" | "assignee";
  order?: "asc" | "desc";
  limit?: number;
  offset?: number;
}

export interface Page<T> {
  items: T[];
  total: number; // Treffer VOR limit/offset - braucht der Client zum Blättern
}

export class TicketRepository extends Repository<Ticket> {
  find(query: TicketQuery): Page<Ticket> {
    let result = this.getAll().filter(
      (t) =>
        (!query.status || t.status === query.status) &&
        (!query.assignee || t.assignee === query.assignee)
    );
    if (query.sort) {
      const key = query.sort;
      const direction = query.order === "desc" ? -1 : 1;
      result = [...result].sort((a, b) => a[key].localeCompare(b[key]) * direction);
    }
    const total = result.length;
    const offset = query.offset ?? 0;
    const end = query.limit === undefined ? undefined : offset + query.limit;
    return { items: result.slice(offset, end), total };
  }
}
```

`[...result].sort(...)`: `sort` sortiert **an Ort und Stelle**. Ohne die Kopie würde die Reihenfolge im Repository selbst verändert.

## Aufgabe 5: Route

```ts
// backend/src/routes/ticket-routes.ts
router.get("/", (req, res) => {
  const query = validate(listQuerySchema, req.query);
  const page = repository.find(query);
  res.set("X-Total-Count", String(page.total));
  res.status(200).json(page.items);
});
```

## Aufgabe 6: Gemessene Antworten (09/2026)

Nach zwei zusätzlichen Tickets ("API dokumentieren" für Sam, "Backup einrichten" für Alex):

```text
GET /tickets
  -> 200 X-Total-Count: 5   [Setup Repo | Add CI pipeline | Containerize backend | API dokumentieren | Backup einrichten]
GET /tickets?status=To%20Do
  -> 200 X-Total-Count: 3   [Setup Repo | API dokumentieren | Backup einrichten]
GET /tickets?assignee=Alex&sort=title
  -> 200 X-Total-Count: 3   [Backup einrichten | Containerize backend | Setup Repo]
GET /tickets?sort=title&order=desc&limit=2
  -> 200 X-Total-Count: 5   [Setup Repo | Containerize backend]
GET /tickets?sort=title&order=desc&limit=2&offset=2
  -> 200 X-Total-Count: 5   [Backup einrichten | API dokumentieren]
GET /tickets?status=Todo
  -> 422  {"error":"validation failed","details":[{"field":"status","message":"Invalid option: expected one of \"To Do\"|\"In Progress\"|\"Done\""}]}
GET /tickets?limit=abc
  -> 422  {"error":"validation failed","details":[{"field":"limit","message":"Invalid input: expected number, received NaN"}]}
GET /tickets?stauts=Done
  -> 422  {"error":"validation failed","details":[{"field":"(root)","message":"Unrecognized key: \"stauts\""}]}
```

`X-Total-Count` bleibt beim Blättern bei 5 - die Zahl der Treffer, nicht die Länge der Seite.

## Commit

```bash
git add -A
git commit -m "feat: GET /tickets mit Filter, Sortierung, Paginierung und X-Total-Count"
```

## Grenzen

- Ohne `limit` liefert die API weiterhin alles, damit bestehende Clients laufen. In Produktion würde man eine Standard-Seitengröße erzwingen.
- Soll ein Browser-Frontend `X-Total-Count` lesen, muss der Server den Header per CORS freigeben (`exposedHeaders`). Das wird am Freitag relevant, sobald das Frontend blättern soll.
- `limit`/`offset` wird bei großen Datenmengen langsam, weil die Datenbank die übersprungenen Einträge trotzdem durchgeht. Die Alternative heißt Cursor-Paginierung ("gib mir 20 nach ID X").
