# Modul 21: Cloud-Deployment (Trainer-Demo)

## Lab 21.1 - Azure-Deployment-Grundlagen

---

## Lab-Ziel

Du kennst die grundlegenden Konzepte, die nötig sind, um eine statische Web-Anwendung (wie das React-Frontend aus Modul 18/19) in eine Cloud-Umgebung wie Azure zu bringen.

**Hinweis:** Dieses Lab ist eine reine Trainer-Demo ohne eigene Teilnehmerübung.

---

## Vom lokalen Build zum Cloud-Deployment

```bash
# frontend/ - Produktions-Build erzeugen (dieselbe Vite-App aus Modul 18/19)
cd frontend
npm run build
# erzeugt frontend/dist/ mit statischen HTML/CSS/JS-Dateien
```

- `npm run build` erzeugt genau die Art von statischen Dateien, die eine Cloud-Plattform wie Azure Static Web Apps direkt ausliefern kann - kein Node-Server nötig für das Frontend selbst.
- Das Backend (Express + MongoDB, Modul 11-16) bräuchte für eine echte Cloud-Bereitstellung einen separaten Hosting-Dienst (z. B. Azure App Service oder Azure Container Apps) - das ist bewusst nicht Teil dieser Demo.

## Grundbegriffe

| Begriff           | Bedeutung                                                                                 |
| ----------------- | ----------------------------------------------------------------------------------------- |
| Static Web App    | Azure-Dienst speziell für statische Frontend-Builds (HTML/CSS/JS)                         |
| CI/CD-Integration | GitHub Actions kann bei jedem Push automatisch bauen und deployen (Anknüpfung an Modul 4) |
| Custom Domain     | eigene Domain statt der von Azure vergebenen Standard-URL                                 |

---

## Live-Demo-Ablauf (durch den Trainer)

1. `npm run build` im `frontend/`-Ordner live ausführen und den Inhalt von `dist/` zeigen.
2. Kurz erläutern, dass dieselbe GitHub-Actions-Pipeline aus Modul 4 grundsätzlich um einen Deployment-Schritt erweiterbar wäre (ohne dies tatsächlich einzurichten).

## Checkpoint

Die Teilnehmenden können erklären, warum ein reines Frontend-Build-Ergebnis (`dist/`) einfacher zu hosten ist als eine vollständige Backend-Anwendung mit Datenbankanbindung.

Weiter geht es mit Lab 21.2: Azure Static Web Apps im Detail.
