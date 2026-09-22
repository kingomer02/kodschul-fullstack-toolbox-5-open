# Lab 19.9 - Übung: Context für die Anmeldung

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - die Anmeldung wandert aus `App` in einen `AuthProvider`.

## Ausgangslage

- Board mit `useReducer` aus Lab 19.8. Der Token liegt als State in `App`, `LoginForm` bekommt `onLoggedIn` als Prop.

## Aufgaben

1. **Bestandsaufnahme:** Welche Komponenten brauchen heute den Token oder den Login - und über wie viele Ebenen wird etwas dafür durchgereicht?
2. Neue Anforderung: Über dem Board soll "Angemeldet als *name*" mit einem Button "Abmelden" stehen, als eigene Komponente `UserBar`. Überlege: Wie käme sie ohne Context an Name und Logout?
3. Lege `src/auth/AuthContext.tsx` an: Context, `AuthProvider` (hält Token und Benutzernamen, bietet `login` und `logout`) und einen Hook `useAuth()`.
4. Wickle `<App />` in `main.tsx` in den Provider.
5. Stelle `LoginForm`, `App` und die neue `UserBar` auf `useAuth()` um. `LoginForm` braucht danach keine Props mehr.
6. Teste: Anmelden, Board sehen, Abmelden, erneut anmelden.
7. **Überlegung:** Warum steckt der Wert des Providers in `useMemo`? Und warum gehört die Ticketliste **nicht** in einen Context?

## Checkpoint

- "Angemeldet als alex · Abmelden" erscheint über dem Board.
- "Abmelden" zeigt wieder das Login-Formular.
- `useAuth()` außerhalb des Providers wirft eine verständliche Fehlermeldung.

## Abschlusskriterien

- Keine Komponente bekommt mehr einen Token oder einen Login-Callback als Prop.
- Du kannst zwei Fälle nennen, in denen du **keinen** Context nehmen würdest.

## Fallback

Falls TypeScript bei `useContext` meckert, der Wert könne `null` sein: Genau dafür ist die Prüfung in `useAuth()` da - danach ist der Typ eindeutig.

## Hinweis zum Linter

`npm run lint` warnt `only-export-components`, weil `AuthContext.tsx` eine Komponente **und** einen Hook exportiert. Das betrifft nur das schnelle Neuladen im Entwicklungsmodus. Wer es sauber will, legt `useAuth` in eine eigene Datei.
