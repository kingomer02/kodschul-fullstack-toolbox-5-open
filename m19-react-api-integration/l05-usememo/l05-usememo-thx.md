# Modul 19: React trifft die gesicherte API

## Lab 19.5 - Vertiefung Hooks (2/6): `useMemo`

---

## Lab-Ziel

Jedes Rendern führt die ganze Komponenten-Funktion aus - auch Berechnungen, deren Ergebnis sich gar nicht geändert hat. `useMemo` merkt sich ein Ergebnis und rechnet nur neu, wenn sich bestimmte Werte ändern. Du misst, **wann** sich das lohnt und wann nicht.

**Leitfragen:**

<details>
<summary>Was genau merkt sich `useMemo`?</summary>

Das **Ergebnis** einer Funktion, zusammen mit den Werten im Abhängigkeitsarray. Beim nächsten Rendern vergleicht React jede Abhängigkeit mit `Object.is` (für Objekte und Arrays: gleiche **Referenz**?). Ist alles gleich, bekommt man das alte Ergebnis zurück, die Funktion läuft gar nicht.

</details>

<details>
<summary>Warum nicht einfach alles in `useMemo` packen?</summary>

Weil es selbst etwas kostet: Speicher für das alte Ergebnis, den Vergleich der Abhängigkeiten, und Code, der schwerer zu lesen ist. Bei einer Berechnung über drei Tickets ist `useMemo` teurer als das Rechnen selbst. Und eine vergessene Abhängigkeit liefert **veraltete** Ergebnisse - ein echter Fehler.

</details>

---

## Syntax

```tsx
const columns = useMemo(() => {
  // teure Berechnung
  return result;
}, [tickets, search]);   // neu rechnen nur, wenn sich eines davon ändert
```

## Wann `useMemo` hilft - und wann nicht

| Situation | Hilft `useMemo`? |
|---|---|
| Komponente rendert wegen **anderer** Werte neu, die Berechnung hängt nicht davon ab | **ja** - das ist der Hauptfall |
| Eine Abhängigkeit ändert sich (z. B. der Suchbegriff) | nein - dann muss ohnehin neu gerechnet werden |
| Berechnung über wenige Elemente | nein - der Overhead ist größer als der Gewinn |
| Ergebnis wird an eine mit `memo` geschützte Kind-Komponente übergeben | ja - wegen der gleichbleibenden **Referenz** (Lab 19.6) |

## Messen statt raten

Die React-Dokumentation empfiehlt: erst messen, dann optimieren. Werkzeuge:
- `performance.now()` vor und nach der Berechnung
- DevTools → Performance → **CPU-Drosselung** (z. B. 4x), um ein langsameres Gerät zu simulieren. Euer Entwicklerrechner ist nicht das Notebook eurer Nutzer.
- Richtwert: **16 ms** pro Bild bei 60 Bildern pro Sekunde. Alles, was ein Rendering darüber hinaus verlängert, ruckelt.

---

## Brücke zu dem, was du kennst

`useMemo` ist ein Cache mit automatischer Invalidierung, vergleichbar mit Springs `@Cacheable` - nur pro Komponente, und der Schlüssel sind die Abhängigkeiten. Dieselbe Frage wie beim Cachen im Backend: Ist das Rechnen teuer genug, dass sich der Cache lohnt?

---

## Checkpoint

Du kannst mit einer Messung belegen, bei welcher Datenmenge und welcher CPU-Leistung `useMemo` in deinem Board spürbar wird.

## Projektbezug

Das Board bekommt eine Suche und einen Schalter für die Zähler in den Spaltenköpfen. Beides bleibt über die weiteren Labs erhalten.
