# Modul 10: Einführung in Container

## Lab 10.2 - Container vs. virtuelle Maschinen

---

## Lab-Ziel

Du kannst erklären, worin sich Container und virtuelle Maschinen unterscheiden, und die Konsequenzen für TeamBoard einschätzen.

**Leitfragen:**

<details>
<summary>Was teilt sich ein Container mit dem Host-System, was eine VM nicht teilt?</summary>

Ein Container teilt sich den Host-Kernel; eine VM bringt einen eigenen, vollständigen Gastbetriebssystem-Kernel mit.

</details>

<details>
<summary>Warum starten Container typischerweise in Millisekunden bis Sekunden, VMs aber in Minuten (oder zumindest deutlich länger)?</summary>

Ein Container startet nur den Anwendungsprozess auf einem bereits laufenden Kernel; eine VM muss zusätzlich ein komplettes Betriebssystem hochfahren.

</details>

<details>
<summary>Welche Konsequenz hat die gemeinsame Kernel-Nutzung für die Isolation von Containern?</summary>

Container isolieren Prozesse, Netzwerk und Dateisystem über Kernel-Mechanismen (Namespaces/Cgroups), sind aber grundsätzlich weniger stark isoliert als VMs, die eine eigene Kernel-Grenze haben.

</details>

---

## Container vs. VM im Vergleich

| Merkmal           | Container                               | Virtuelle Maschine                    |
| ----------------- | --------------------------------------- | ------------------------------------- |
| Kernel            | geteilt mit Host                        | eigener Gast-Kernel                   |
| Startzeit         | Millisekunden bis Sekunden              | Sekunden bis Minuten                  |
| Ressourcenbedarf  | gering (nur Anwendung + Abhängigkeiten) | hoch (vollständiges Betriebssystem)   |
| Isolation         | Prozess-Ebene (Namespaces/Cgroups)      | Hardware-nahe Virtualisierung         |
| Typischer Einsatz | einzelne Anwendungsdienste              | vollständig getrennte Betriebssysteme |

---

## Warum das für TeamBoard relevant ist

- Backend, Frontend und MongoDB laufen ab Modul 11-13 als **separate, leichtgewichtige Container**, nicht als eine gemeinsame VM.
- Schnelle Start-/Stoppzeiten machen es praktikabel, die gesamte Umgebung mehrmals täglich neu zu starten (z. B. nach Codeänderungen).

**Grenze:** Container sind kein vollständiger Sicherheits-Ersatz für VMs, wenn völlig isolierte, gegenseitig misstrauende Umgebungen nötig sind - für ein Kursprojekt wie TeamBoard ist die Prozess-Isolation von Containern ausreichend.

---

## Checkpoint

Der Unterschied zwischen Container und VM wurde anhand von Startzeit, Ressourcenbedarf und Isolation erklärt und auf die geplante TeamBoard-Container-Architektur (Backend/Frontend/MongoDB) bezogen.

Weiter geht es mit Lab 10.3: Überblick über das Container-Ökosystem.
