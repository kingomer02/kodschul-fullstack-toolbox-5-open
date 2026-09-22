# Modul 19: React trifft die gesicherte API

## Lab 19.9 - Vertiefung Hooks (6/6): Context für die Anmeldung

---

## Lab-Ziel

Der Token liegt in `App` und muss überall hin, wo eine Anfrage an die API geht - notfalls über mehrere Ebenen, die ihn selbst gar nicht brauchen ("Prop Drilling"). Context stellt einen Wert **allen** Komponenten darunter zur Verfügung. Du baust einen `AuthProvider` mit einem eigenen Hook `useAuth()` - und eine Leiste "Angemeldet als … · Abmelden".

**Leitfragen:**

<details>
<summary>Wann Context - und wann nicht?</summary>

Für Werte, die **viele** Komponenten auf **verschiedenen** Ebenen brauchen und die sich **selten** ändern: angemeldeter Benutzer, Sprache, Farbschema. Nicht für Daten, die sich ständig ändern (die Ticketliste, ein Suchfeld): Jede Änderung am Context-Wert rendert **alle** Komponenten neu, die ihn lesen.

</details>

<details>
<summary>Warum einen eigenen Hook `useAuth()` statt `useContext(AuthContext)` überall?</summary>

Er versteckt, **wie** die Anmeldung gespeichert ist, und kann prüfen, dass es überhaupt einen Provider gibt. Aufrufer schreiben `const { token } = useAuth();` und müssen nichts über Context wissen. Eigene Hooks sind in React der Weg, Logik wiederzuverwenden - wie eine Service-Klasse.

</details>

---

## Die drei Teile

```tsx
// 1 · Context anlegen
const AuthContext = createContext<AuthValue | null>(null);

// 2 · Provider: hält den Zustand und stellt ihn bereit
export function AuthProvider({ children }: { children: ReactNode }) {
  const [session, setSession] = useState(...);
  const value = useMemo(() => ({ ... }), [session]);
  return <AuthContext value={value}>{children}</AuthContext>;    // React 19
}

// 3 · Hook zum Lesen
export function useAuth() {
  const auth = useContext(AuthContext);
  if (!auth) throw new Error("useAuth() nur innerhalb von <AuthProvider>");
  return auth;
}
```

In React 19 ist der Context selbst der Provider. In älterem Code und Anleitungen steht `<AuthContext.Provider value={...}>` - das funktioniert weiterhin.

**Warum `useMemo` für `value`:** Sonst ist `value` bei jedem Rendern des Providers ein neues Objekt, und jede Komponente mit `useAuth()` rendert mit - dasselbe Referenz-Thema wie in Lab 19.6.

---

## Brücke zu dem, was du kennst

Context ist die React-Antwort auf Dependency Injection: Eine Komponente fordert einen Wert an, statt ihn durchgereicht zu bekommen. Angular (Modul 20) hat dafür einen eingebauten Injektor mit Services - in React sind es Context und eigene Hooks. Und `useAuth()` entspricht in etwa `SecurityContextHolder` in Spring.

---

## Checkpoint

Nach dem Login steht "Angemeldet als alex" über dem Board, "Abmelden" führt zurück zum Login-Formular. `LoginForm` bekommt keine Props mehr.

## Projektbezug

Das ist der Endstand des Frontends für die Abschluss-Demo in Modul 22.
