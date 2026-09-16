# Modul 18: Einstieg in React

## Lab 18.3 - React-Projekt-Setup für TeamBoard

---

## Lab-Ziel

Du richtest ein echtes Vite-React-TS-Projekt im `frontend/`-Ordner ein, übernimmst Bootstrap und das eigene Sass aus Modul 17, und rendert damit erstmals das vollständige Drei-Spalten-Board als React-Komponentenbaum.

**Leitfragen:**

<details>
<summary>Warum wird der bisherige statische `frontend/index.html`-Stand (Modul 17) durch das Vite-Projekt ersetzt, statt ihn unverändert weiterzuverwenden?</summary>

Vite bringt sein eigenes Build-System und eine eigene `index.html` als Einstiegspunkt mit; die React-Komponenten übernehmen ab jetzt die Darstellung, die zuvor rein statisches HTML erledigt hat.

</details>

<details>
<summary>Warum lassen sich `main.scss` und die Bootstrap-CSS-Datei aus Modul 17 unverändert in das React-Projekt übernehmen?</summary>

CSS-Regeln sind unabhängig davon gültig, ob das HTML statisch oder von React erzeugt wurde - Klassen wie `.card` oder `.column` wirken in beiden Fällen gleich, solange dieselben Klassennamen in JSX verwendet werden.

</details>

---

## Vite-Projekt einrichten

```bash
npm create vite@latest frontend -- --template react-ts
cd frontend
npm install
npm install bootstrap
```

```ts
// frontend/src/main.tsx (Ergänzung der Imports)
import "bootstrap/dist/css/bootstrap.min.css";
import "./styles/main.scss";
```

- Die `main.scss`-Datei aus Modul 17 (inkl. Farbvariablen für `.column.todo/.in-progress/.done`) wird unverändert nach `frontend/src/styles/main.scss` übernommen; Vite kompiliert `.scss` automatisch, ein eigenes Gulp benötigt das React-Projekt nicht mehr.

## Vollständiges Board rendern

```tsx
// frontend/src/App.tsx
import { Column } from "./components/Column";
import { sampleTickets } from "./data/sample-tickets";

function App() {
  return (
    <div className="container-fluid">
      <div className="row">
        <div className="col-12 col-md-4 column todo">
          <Column title="To Do" initialTickets={sampleTickets.todo} />
        </div>
        <div className="col-12 col-md-4 column in-progress">
          <Column
            title="In Progress"
            initialTickets={sampleTickets.inProgress}
          />
        </div>
        <div className="col-12 col-md-4 column done">
          <Column title="Done" initialTickets={sampleTickets.done} />
        </div>
      </div>
    </div>
  );
}

export default App;
```

```ts
// frontend/src/data/sample-tickets.ts
export const sampleTickets = {
  todo: [{ id: "t-1", title: "Login-Formular bauen", assignee: "Alex" }],
  inProgress: [{ id: "t-2", title: "API anbinden", assignee: "Sam" }],
  done: [],
};
```

---

## Checkpoint

`npm run dev` zeigt das vollständige Drei-Spalten-Board mit Bootstrap- und Sass-Styling aus Modul 17, gerendert über React-Komponenten statt über statisches HTML.

## Projektbezug

Das Board zeigt weiterhin nur hartcodierte Beispieldaten. Modul 19 verbindet es mit der echten, durch JWT abgesicherten REST-API aus Modul 14/16.
