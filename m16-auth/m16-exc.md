# Transfer-Übung Modul 16 - Übung: Kompletten Auth-Flow end-to-end nachvollziehen

**Dauer:** ca. 25 Minuten
**Ändert die TeamBoard-Projektbasis?** Nein - nutzt die bestehende, jetzt abgesicherte API rein über Anfragen.

## Ziel

Registrierung, Login und Ticketzugriff als einen zusammenhängenden Ablauf nachvollziehen und dabei bewusst mehrere Fehlerfälle provozieren.

## Ausgangslage

- Backend läuft containerisiert mit aktivierter Auth-Middleware auf `/tickets`.

## Aufgaben

1. Registriere einen neuen, noch nicht existierenden Nutzer.
2. Versuche, denselben Nutzernamen ein zweites Mal zu registrieren - notiere den erhaltenen Statuscode.
3. Logge dich mit dem neuen Nutzer ein und speichere den Token.
4. Lege mit diesem Token per `POST /tickets` ein Ticket an und weise es per `PATCH /tickets/:id/assign` demselben Nutzernamen zu.
5. Warte (oder stelle dir vor, der Token wäre abgelaufen) und teste eine Anfrage mit einem absichtlich verstümmelten Token gegen `GET /tickets` - notiere den Statuscode.
6. Fasse in 2-3 Sätzen zusammen, welche drei Statuscodes (`201`/`400`, `200`/`401`, `200`/`401`) in diesem Ablauf jeweils "korrekt" sind und warum.

## Checkpoint

- Schritt 2 liefert `400` (Nutzername bereits vergeben).
- Schritt 4 liefert für beide Anfragen Erfolgscodes (`201`/`200`).
- Schritt 5 liefert `401`.

## Abschlusskriterien

- Die Zusammenfassung aus Aufgabe 6 nennt für jeden Schritt den erwarteten Code und eine kurze Begründung.

## Lösungshinweise

```bash
curl -X POST http://localhost:3000/auth/register \
  -H "Content-Type: application/json" -d '{"username": "sam", "password": "geheim123"}'
# 201

curl -X POST http://localhost:3000/auth/register \
  -H "Content-Type: application/json" -d '{"username": "sam", "password": "irgendwas"}'
# 400 { "error": "username already taken" }

TOKEN=$(curl -s -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username": "sam", "password": "geheim123"}' | jq -r .token)

curl -X POST http://localhost:3000/tickets \
  -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
  -d '{"title": "End-to-End-Ticket"}'
# 201, id merken

curl -X PATCH http://localhost:3000/tickets/<id>/assign \
  -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
  -d '{"assignee": "sam"}'
# 200

curl http://localhost:3000/tickets -H "Authorization: Bearer $TOKEN-verstümmelt"
# 401
```

## Fallback

Falls kein `jq` verfügbar ist: den Token manuell aus der Login-Antwort kopieren, statt ihn per Kommandozeile zu extrahieren.
