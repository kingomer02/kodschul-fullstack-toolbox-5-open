# React-Hooks: Welcher wann?

Nachschlagewerk zu den Labs 19.4–19.9. Alle Zahlen stammen aus Messungen am TeamBoard (09/2026).

## Die Grundlage: Wann rendert eine Komponente?

1. Ihr **eigener State** ändert sich.
2. Ihre **Eltern-Komponente** rendert - dann rendern alle Kinder mit.
3. Ein **Context**, den sie liest, ändert sich.

Im Entwicklungsmodus rendert `<StrictMode>` alles doppelt. Gemessen wird im Production-Build (`npm run build && npm run preview`).

## Entscheidungstabelle

| Du willst … | Nimm | Nicht |
|---|---|---|
| einen Wert anzeigen, der sich ändert | `useState` | `useRef` - die Anzeige aktualisiert sich nicht |
| etwas, das sich aus Props/State **berechnen** lässt | eine normale Variable | `useState` - bleibt beim ersten Wert stehen (Lab 19.4) |
| eine **teure** Berechnung nicht bei jedem Rendern wiederholen | `useMemo` | `useMemo` bei 3 Elementen - kostet mehr als es spart |
| Kind-Komponenten überspringen, deren Props gleich sind | `memo` am Kind **+** `useCallback`/`useMemo` für Funktionen/Objekte in den Props | `memo` allein - neue Funktionen machen es wirkungslos (Lab 19.6) |
| ein DOM-Element ansprechen (Fokus, Scrollen, Maße) | `useRef` | `document.querySelector` |
| etwas merken, ohne neu zu rendern (Timer-ID, Zähler) | `useRef` | `useState` - im Rendern gesetzt: Endlosschleife |
| mit der Außenwelt synchronisieren (Listener, Timer, `fetch`) | `useEffect` **mit Aufräumfunktion** | `useEffect` ohne Aufräumen - Listener sammeln sich (Lab 19.7) |
| mehrere zusammengehörige Werte, die sich gemeinsam ändern | `useReducer` | viele einzelne `useState`, die man synchron halten muss |
| einen Wert vielen Komponenten auf vielen Ebenen geben, der sich selten ändert | Context + eigener Hook | Context für Daten, die sich ständig ändern |
| Logik zwischen Komponenten wiederverwenden | eigener Hook (`useAuth`, …) | Copy-Paste |

## Gemessen am TeamBoard

| Lab | Messung | Ergebnis |
|---|---|---|
| 19.4 | Board mit `useState(initialTickets)` nach dem Login | leer, obwohl die Tickets geladen wurden |
| 19.4 | Renderings bei einem Tastendruck im Formular | nur das Formular (1) |
| 19.5 | Umschalten ohne `useMemo`, 20.000 Tickets | 3,5 ms, mit 4x CPU-Drosselung 15 ms |
| 19.5 | Umschalten mit `useMemo` | nicht neu berechnet |
| 19.6 | neu gerenderte Karten beim Umschalten: ohne `memo` / `memo` allein / `memo` + `useCallback` | 60 / 40 / 0 |
| 19.7 | Handler-Aufrufe ohne Aufräumfunktion (dev) | 2 pro Tastendruck |
| 19.8 | Anfragen und Karten pro "Weiter →": Liste neu laden / `useReducer` | 2 und 3 / 1 und 1 |

## Die Regeln der Hooks

- Hooks nur **ganz oben** in einer Komponente oder einem eigenen Hook aufrufen - nie in `if`, Schleifen oder nach einem `return`. React erkennt Hooks an ihrer **Reihenfolge**.
- Eigene Hooks heißen `use…`, sonst erkennt der Linter sie nicht.
- Das Abhängigkeitsarray ist keine Optimierung, sondern eine **Aussage**: "Dieser Code benutzt diese Werte." Fehlt einer, arbeitet der Code mit veralteten Werten.

## Faustregel für Optimierungen

Erst messen, dann `useMemo`/`memo`/`useCallback`. Der Entwicklerrechner ist nicht das Notebook der Nutzer - mit CPU-Drosselung messen. Das Budget für ein flüssiges Bild sind 16 ms.
