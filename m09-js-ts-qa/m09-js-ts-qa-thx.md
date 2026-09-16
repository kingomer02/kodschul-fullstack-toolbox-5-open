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
3. **Zusatzübung (falls Zeit vorhanden):** ein weiteres, kleines Beispiel analog zu `TicketRepository`/`Repository<T>` gemeinsam erweitern, z. B. eine Methode `remove(id: string): void` ergänzen.
4. **Offene Fragen sammeln:** Punkte, die erst mit Docker/API-Kontext (ab Modul 10) beantwortbar sind, werden notiert und dort wieder aufgegriffen.

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
