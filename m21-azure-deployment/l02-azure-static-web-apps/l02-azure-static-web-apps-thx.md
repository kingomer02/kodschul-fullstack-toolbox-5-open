# Modul 21: Cloud-Deployment (Trainer-Demo)

## Lab 21.2 - Azure Static Web Apps

---

## Lab-Ziel

Du kennst den grundsätzlichen Ablauf, wie ein GitHub-Repository (wie das TeamBoard-Projekt) über Azure Static Web Apps automatisch bereitgestellt werden kann.

**Hinweis:** Dieses Lab ist eine reine Trainer-Demo ohne eigene Teilnehmerübung - es wird keine echte Azure-Ressource für den Kurs angelegt.

---

## Ablauf einer Azure-Static-Web-Apps-Bereitstellung (konzeptionell)

1. Ein Azure-Static-Web-Apps-Dienst wird mit dem GitHub-Repository verknüpft.
2. Azure legt automatisch eine GitHub-Actions-Workflow-Datei an, die bei jedem Push den Build-Befehl (`npm run build`) ausführt und den Inhalt von `dist/` bereitstellt.
3. Nach jedem Push auf den konfigurierten Branch ist die aktuelle Version automatisch unter einer von Azure vergebenen URL erreichbar.

```yaml
# Beispielhafter, von Azure generierter Workflow-Ausschnitt (nur zur Veranschaulichung)
- name: Build and Deploy
  uses: Azure/static-web-apps-deploy@v1
  with:
    app_location: "frontend"
    output_location: "dist"
```

- `app_location`/`output_location` entsprechen genau dem `frontend/`-Ordner und dem `dist/`-Build-Ergebnis aus Lab 21.1.

---

## Grenzen dieser Demo

- Das Backend (Express + MongoDB + JWT-Auth) ist **nicht** Teil dieser Static-Web-App-Demo - eine reale Bereitstellung bräuchte einen zusätzlichen Dienst für das Backend sowie eine gehostete MongoDB-Instanz (z. B. Azure Cosmos DB oder MongoDB Atlas), was den Rahmen dieses Kurses übersteigt.
- Es wird in diesem Kurs keine echte Azure-Ressource angelegt - die Demo bleibt konzeptionell.

---

## Live-Demo-Ablauf (durch den Trainer)

1. Die Azure-Portal-Oberfläche zeigen (Screenshot oder Live-Zugang, falls vorhanden) und den Schritt "Static Web App erstellen" durchgehen.
2. Den automatisch generierten GitHub-Actions-Workflow zeigen und mit der bestehenden `ci.yml` aus Modul 4/13 vergleichen.

## Checkpoint

Die Teilnehmenden können den Unterschied zwischen dem Deployment des Frontends (Static Web Apps, in dieser Demo gezeigt) und dem Deployment des Backends (nicht Teil dieser Demo) benennen.

## Projektbezug

Damit ist der konzeptionelle Blick über TeamBoard hinaus abgeschlossen. Modul 22 fasst das gesamte Projekt in einer abschließenden Live-Demo zusammen.
