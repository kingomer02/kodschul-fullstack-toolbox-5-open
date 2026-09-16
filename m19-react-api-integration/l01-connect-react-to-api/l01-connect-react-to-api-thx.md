# Modul 19: React trifft die gesicherte API

## Lab 19.1 - Eine Komponente an eine öffentliche Test-API anbinden

---

## Lab-Ziel

Du kannst mit `useEffect` und `fetch` Daten von einer öffentlichen Test-API laden und in einer Komponente anzeigen, als Vorbereitung auf die echte TeamBoard-API in Lab 19.2.

**Leitfragen:**

<details>
<summary>Warum steht der `fetch`-Aufruf in einem `useEffect` statt direkt im Komponentenkörper?</summary>

Ohne `useEffect` würde bei jedem Rendern ein neuer Netzwerkaufruf ausgelöst - `useEffect` mit leerem Abhängigkeitsarray (`[]`) sorgt dafür, dass der Aufruf nur einmal beim ersten Rendern passiert.

</details>

<details>
<summary>Warum braucht die Komponente einen eigenen `loading`-Zustand?</summary>

Der Netzwerkaufruf dauert eine gewisse Zeit - ohne `loading`-Zustand würde die Komponente kurzzeitig mit leeren oder `undefined`-Daten rendern, bevor die Antwort eintrifft.

</details>

---

## Minimalbeispiel: Daten laden

```tsx
// sample-fetch/src/UserList.tsx
import { useEffect, useState } from "react";

interface User {
  id: number;
  name: string;
}

export function UserList() {
  const [users, setUsers] = useState<User[]>([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then((data: User[]) => {
        setUsers(data);
        setLoading(false);
      });
  }, []);

  if (loading) return <p>Lädt...</p>;

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

---

## Checkpoint

Beim ersten Rendern zeigt die Komponente kurz "Lädt...", danach die Namensliste - beobachtbar in den Entwicklertools über die Netzwerk-Anfrage an `jsonplaceholder.typicode.com`.

Weiter geht es mit Lab 19.2: dieselbe Technik für die echte, gesicherte TeamBoard-API.
