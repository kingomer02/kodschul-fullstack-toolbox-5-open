# Modul 9: Puffer für offene JavaScript/TypeScript-Fragen

---

## Ziel dieses Moduls

Dieses Modul ist bewusst kein neuer Lerninhalt, sondern ein kalibrierter Puffer: offene Fragen aus den Modulen 5-8 (Node.js, TypeScript-Grundlagen, TypeScript-OOP) werden aufgegriffen, bevor am Nachmittag von Tag 3 an mit Docker weitergearbeitet wird.

**Dauer:** bis zu 90 Minuten, abhängig vom tatsächlichen Bedarf der Gruppe.
**Ändert die TeamBoard-Projektbasis?** Nein.

---

## Ablauf

1. **Kurzumfrage (5-10 Min):** Wo hakt es noch - Basistypen, Interfaces, Klassen/Vererbung, Access Modifiers oder Generics?
2. **Gezielte Wiederholung:** je nach Rückmeldung 1-2 der vorherigen Labs (Modul 7/8) gemeinsam nochmals durchgehen, mit Fokus auf die zuvor unklaren Stellen.
3. **Zusatzübung (falls Zeit vorhanden):** siehe ausgearbeitetes Beispiel unten - `remove(id: string): void` in `Repository<T>` ergänzen und in `TicketService` nutzen.
4. **Offene Fragen sammeln:** Punkte, die erst mit Docker/API-Kontext (ab Modul 10) beantwortbar sind, werden notiert und dort wieder aufgegriffen.

---

## Ausgearbeitete Zusatzübung: `remove()` ergänzen

Falls Zeit bleibt, wird `Repository<T>` (Modul 8, Lab 8.3) um eine Löschmethode erweitert - das verbindet Generics, Access Modifiers und `TicketService` in einer einzigen kleinen Aufgabe.

**Aufgabe:** Ergänze `Repository<T extends { id: string }>` um `remove(id: string): boolean`, das `true` zurückgibt, wenn ein Element entfernt wurde, sonst `false`. Ergänze anschließend `TicketService` um `deleteTicket(id: string): boolean`, die diese Methode nutzt.

**Lösung:**

```ts
// backend/src/repositories/repository.ts
export class Repository<T extends { id: string }> {
  private items: T[] = [];

  add(item: T): void {
    this.items.push(item);
  }

  findById(id: string): T | undefined {
    return this.items.find((item) => item.id === id);
  }

  remove(id: string): boolean {
    const index = this.items.findIndex((item) => item.id === id);
    if (index === -1) return false;
    this.items.splice(index, 1);
    return true;
  }
}
```

```ts
// backend/src/services/ticket-service.ts (Ergänzung)
deleteTicket(id: string): boolean {
  return this.repository.remove(id);
}
```

**Test:**

```ts
service.deleteTicket("t-1"); // true
service.deleteTicket("t-1"); // false, bereits entfernt
```

---

## Typische Diskussionspunkte

| Thema                  | Typische Unsicherheit                                 |
| ---------------------- | ----------------------------------------------------- |
| `interface` vs. `type` | wann welches verwenden                                |
| `private`/`protected`  | Unterschied in der Praxis, insbesondere bei Vererbung |
| Generics               | wann sich der zusätzliche Aufwand lohnt               |
| `strict: true`         | welche Fehlerklassen dadurch neu auftauchen           |

---

## Checkpoint

Die Gruppe bestätigt, dass sie mit den TypeScript-Grundlagen aus Modul 5-8 sicher genug ist, um ab Modul 10 in Docker containerisierte Umgebungen für dasselbe Backend aufzubauen.

Weiter geht es mit Modul 10: Einführung in Container (WSL 2, Container vs. VM, Container-Ökosystem).
