# Lab 22.1 - Lösung: Projekt-Rückblick

## Aufgabe 1: Zuordnung

| Bereich                | Module |
| ---------------------- | ------ |
| Werkzeuge & Grundlagen | 1-9    |
| Containerisierung      | 10-13  |
| API & Daten            | 14-16  |
| Oberfläche             | 17-19  |
| Ausblick               | 20-21  |

## Aufgabe 2: Demo-Durchlauf

```bash
docker compose up -d --build
cd frontend && npm run dev
```

Im Browser: einloggen, "Demo-Rückblick-Ticket" anlegen, zweimal "Weiter →" klicken → Ticket landet in "Done".

## Aufgabe 3-4: Persönliche Einschätzung (Beispiel)

Beispielhafte Antwort: Die JWT-Absicherung (Modul 16) hat am meisten Konzentration gebraucht, weil mehrere Dateien (Middleware, Routen, Token-Handling) zusammenspielen mussten; das Emmet-Lab (Modul 17.1) war dagegen überraschend schnell verständlich.

## Grenzen

Diese Einschätzungen sind individuell - es gibt keine "richtige" Antwort, entscheidend ist die eigene, begründete Reflexion.
