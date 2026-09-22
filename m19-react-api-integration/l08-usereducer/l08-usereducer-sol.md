# Lab 19.8 - Lösung: `useReducer`

## Aufgabe 2: `api.ts` (Ausschnitt)

```ts
export async function moveToNextStatus(token: string, id: string): Promise<Ticket> {
  const res = await fetch(`${API_URL}/tickets/${id}/status`, {
    method: "PATCH",
    headers: { Authorization: `Bearer ${token}` },
  });
  if (!res.ok) throw new Error("Status konnte nicht geändert werden");
  return res.json(); // die API liefert das geänderte Ticket zurück
}
```

`createTicket` analog: `POST` liefert das neue Ticket mit `201`.

## Aufgabe 3: `board-reducer.ts`

```ts
import type { Ticket } from "./api";

export interface BoardState {
  tickets: Ticket[];
  error: string | null;
}

// Jede Aktion ist ein eigener Typ - TypeScript prüft im switch, dass alle behandelt sind
export type BoardAction =
  | { type: "loaded"; tickets: Ticket[] }
  | { type: "created"; ticket: Ticket }
  | { type: "updated"; ticket: Ticket }
  | { type: "failed"; message: string };

export const initialBoard: BoardState = { tickets: [], error: null };

// Reine Funktion: alter Zustand + Aktion -> neuer Zustand. Kein fetch, kein setState.
export function boardReducer(state: BoardState, action: BoardAction): BoardState {
  switch (action.type) {
    case "loaded":
      return { tickets: action.tickets, error: null };
    case "created":
      return { tickets: [...state.tickets, action.ticket], error: null };
    case "updated":
      return {
        // nur das geänderte Ticket ist ein neues Objekt, alle anderen bleiben dieselben
        tickets: state.tickets.map((t) => (t.id === action.ticket.id ? action.ticket : t)),
        error: null,
      };
    case "failed":
      return { ...state, error: action.message };
  }
}
```

## Aufgabe 4: `App.tsx` (Ausschnitt)

```tsx
const [board, dispatch] = useReducer(boardReducer, initialBoard);
const { tickets } = board;

const loadTickets = useCallback(async (activeToken: string) => {
  dispatch({ type: "loaded", tickets: await fetchTickets(activeToken) });
}, []);

const handleAdvance = useCallback(
  async (id: string) => {
    if (!token) return;
    try {
      // Die Antwort enthält das geänderte Ticket - kein erneutes Laden der Liste nötig
      dispatch({ type: "updated", ticket: await moveToNextStatus(token, id) });
    } catch (err) {
      dispatch({ type: "failed", message: (err as Error).message });
    }
  },
  [token]
);

// im JSX, über dem Formular:
{board.error && <div className="alert alert-danger py-2">{board.error}</div>}
```

`dispatch` ist von React garantiert stabil - er muss nicht ins Abhängigkeitsarray. `loadTickets` wird in `handleAdvance` nicht mehr gebraucht, also fällt es heraus.

## Aufgabe 1, 5, 6: Gemessen (09/2026, Production-Build)

| | Anfragen pro Klick | neu gerenderte Karten |
|---|---|---|
| vorher (Liste neu laden) | 2 (`PATCH` + `GET`) | 3 (`t-2`, `t-1`, `t-3`) |
| mit `useReducer` | **1** (`PATCH`) | **1** (`t-1`) |

```text
Board: To Do: - | In Progress: Add CI pipeline, Setup Repo | Done: Containerize backend
```

**Klick auf ein Demo-Ticket** (`?demo=3`):

```text
Anfragen für einen Klick: 1 | neu gerenderte Karten: 0
Fehlermeldung: Status konnte nicht geändert werden
```

Der Server antwortet `404`, `api.ts` wirft, `App` fängt und schickt `failed` - das Board bleibt unverändert, die Meldung erscheint.

## Commit

```bash
git add -A
git commit -m "refactor: Board-Zustand per useReducer, Aktionen ohne Neuladen der Liste"
```

## Grenzen

Ohne Neuladen sieht das Board nur die **eigenen** Änderungen. Ändert jemand anderes gleichzeitig ein Ticket, merkt es das Board erst beim nächsten Laden. Dafür bräuchte es regelmäßiges Nachladen oder eine Push-Verbindung (WebSocket, Server-Sent Events).
