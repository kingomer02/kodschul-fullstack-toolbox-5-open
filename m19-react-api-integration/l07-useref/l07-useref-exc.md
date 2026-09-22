# Lab 19.7 - Übung: `useRef` und Aufräumen in `useEffect`

**Dauer:** ca. 15 Minuten
**Ändert die TeamBoard-Projektbasis?** Ja - die Taste `/` fokussiert das Suchfeld.

## Ausgangslage

- Board mit Suche aus Lab 19.5/19.6.

## Aufgaben

1. Wie bei GitHub: Drückt man `/` irgendwo auf der Seite (nicht in einem Eingabefeld), springt der Cursor ins Suchfeld. Das `/` selbst soll dabei **nicht** im Feld landen.
2. Überlege, wo der Tastatur-Listener angemeldet wird und wer ihn wieder abmeldet.
3. **Das Experiment:** Lass die Aufräumfunktion weg, setz eine Log-Zeile in den Handler und drück im **Entwicklungsmodus** einmal `/`. Wie oft läuft der Handler - und warum? Danach wieder einbauen.
4. **Gedankenexperiment, dann ausprobieren:** Jemand möchte zählen, wie oft `App` rendert, und schreibt dafür `const [renders, setRenders] = useState(0); setRenders(renders + 1);` direkt in die Komponente. Was passiert? Wie sähe es mit `useRef` aus?

## Checkpoint

- `/` fokussiert die Suche, das Feld bleibt leer.
- Mit Aufräumfunktion läuft der Handler im Entwicklungsmodus einmal pro Tastendruck.

## Abschlusskriterien

- Du kannst erklären, warum ein Render-Zähler kein State sein darf.
- Du kannst drei Dinge nennen, die in einem Effekt aufgeräumt werden müssen.

## Fallback

Falls `/` trotzdem im Feld landet: `event.preventDefault()` verhindert, dass der Browser das Zeichen einfügt, nachdem der Fokus gewechselt hat.
