# Lab 19.9 - Lösung: Context für die Anmeldung

## Aufgabe 1-2: Bestandsaufnahme

- `App` hält den Token und reicht `setToken` als `onLoggedIn` an `LoginForm`.
- Wer den Token für Anfragen braucht (`App`, in der Material-Fassung auch `TicketCard` und `NewTicketForm`), bekommt ihn über `App` und `Column` durchgereicht - `Column` selbst braucht ihn nie.
- Eine `UserBar` bräuchte ohne Context zwei weitere Props von `App`: Name und Logout. Und `App` müsste sich den Namen dafür zusätzlich merken.

## Aufgabe 3: `src/auth/AuthContext.tsx`

```tsx
import { createContext, useCallback, useContext, useMemo, useState } from "react";
import type { ReactNode } from "react";
import { login as apiLogin } from "../api";

interface AuthValue {
  token: string | null;
  username: string | null;
  login: (username: string, password: string) => Promise<void>;
  logout: () => void;
}

const AuthContext = createContext<AuthValue | null>(null);

export function AuthProvider({ children }: { children: ReactNode }) {
  const [session, setSession] = useState<{ token: string; username: string } | null>(null);

  const login = useCallback(async (username: string, password: string) => {
    setSession({ token: await apiLogin(username, password), username });
  }, []);

  const logout = useCallback(() => setSession(null), []);

  // useMemo: sonst ist value bei jedem Rendern ein neues Objekt,
  // und jede Komponente mit useAuth() würde mit neu rendern
  const value = useMemo(
    () => ({ token: session?.token ?? null, username: session?.username ?? null, login, logout }),
    [session, login, logout]
  );

  // React 19: der Context selbst ist der Provider (vorher: <AuthContext.Provider>)
  return <AuthContext value={value}>{children}</AuthContext>;
}

export function useAuth(): AuthValue {
  const auth = useContext(AuthContext);
  if (!auth) throw new Error("useAuth() nur innerhalb von <AuthProvider> verwenden");
  return auth;
}
```

## Aufgabe 4: `main.tsx`

```tsx
import { AuthProvider } from "./auth/AuthContext";

createRoot(document.getElementById("root")!).render(
  <StrictMode>
    <AuthProvider>
      <App />
    </AuthProvider>
  </StrictMode>
);
```

## Aufgabe 5: Die Nutzer

```tsx
// src/components/UserBar.tsx
import { useAuth } from "../auth/AuthContext";

// Braucht Benutzername und Logout - ohne Context müsste App beides durchreichen
export function UserBar() {
  const { username, logout } = useAuth();
  if (!username) return null;
  return (
    <div className="d-flex justify-content-end align-items-center gap-2 mb-3 small">
      Angemeldet als <strong>{username}</strong>
      <button className="btn btn-sm btn-outline-secondary" onClick={logout}>
        Abmelden
      </button>
    </div>
  );
}
```

```tsx
// src/components/LoginForm.tsx (Ausschnitt) - keine Props mehr
export function LoginForm() {
  const { login } = useAuth();
  // ...
  async function handleSubmit(event: React.FormEvent) {
    event.preventDefault();
    setError("");
    try {
      await login(username, password);
    } catch {
      setError("Anmeldung fehlgeschlagen");
    }
  }
```

```tsx
// src/App.tsx (Ausschnitt)
const { token } = useAuth();          // statt useState<string | null>(null)
// ...
<h1 className="h3 mb-4">TeamBoard</h1>
<UserBar />
// ...
<LoginForm />                         // statt <LoginForm onLoggedIn={setToken} />
```

## Aufgabe 6: Gemessen (09/2026)

```text
Leiste:          Angemeldet als alex · Abmelden
Board:           To Do: Setup Repo | In Progress: Add CI pipeline | Done: Containerize backend
nach Abmelden:   Überschrift "Anmelden", Passwortfeld sichtbar, 0 Spalten
Fehler in der Konsole: 0
```

## Aufgabe 7

- **`useMemo` für `value`:** Rendert `AuthProvider` neu, entstünde sonst ein neues Objekt - und jede Komponente mit `useAuth()` würde mit rendern, auch wenn sich an der Anmeldung nichts geändert hat.
- **Keine Ticketliste im Context:** Sie ändert sich bei jeder Aktion. Jede Änderung würde **alle** Leser des Contexts neu rendern. Die Liste gehört dorthin, wo sie gebraucht wird, und wandert als Props nach unten.
- **Weitere Fälle ohne Context:** Werte, die nur eine oder zwei Ebenen tief gebraucht werden (dann sind Props klarer), und alles, was sich bei jeder Eingabe ändert (Suchfelder, Formularfelder).

## Commit

```bash
git add -A
git commit -m "refactor: Anmeldung per AuthContext und useAuth(), UserBar mit Abmelden"
```

## Grenzen

Nach einem Neuladen der Seite ist man weiterhin abgemeldet - der Token liegt nur im Speicher. Mit `localStorage` im `AuthProvider` ließe sich das ändern, an **einer** Stelle. Genau das ist der Vorteil: Wie die Anmeldung gespeichert wird, weiß nur noch der Provider.
