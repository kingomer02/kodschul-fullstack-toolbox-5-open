# Transfer-Übung Modul 16 - Lösung: Kompletten Auth-Flow end-to-end nachvollziehen

## Aufgabe 1: Registrierung

```bash
curl -X POST http://localhost:3000/auth/register \
  -H "Content-Type: application/json" -d '{"username": "sam", "password": "geheim123"}'
# 201 { "username": "sam" }
```

## Aufgabe 2: Doppelte Registrierung

```bash
curl -X POST http://localhost:3000/auth/register \
  -H "Content-Type: application/json" -d '{"username": "sam", "password": "irgendwas"}'
# 400 { "error": "username already taken" }
```

## Aufgabe 3: Login

```bash
TOKEN=$(curl -s -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username": "sam", "password": "geheim123"}' | jq -r .token)
```

## Aufgabe 4: Ticket anlegen und zuweisen

```bash
curl -X POST http://localhost:3000/tickets \
  -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
  -d '{"title": "End-to-End-Ticket"}'
# 201

curl -X PATCH http://localhost:3000/tickets/<id>/assign \
  -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
  -d '{"assignee": "sam"}'
# 200
```

## Aufgabe 5: Verstümmelter Token

```bash
curl http://localhost:3000/tickets -H "Authorization: Bearer ${TOKEN}kaputt"
# 401 { "error": "invalid token" }
```

## Aufgabe 6: Zusammenfassung

Schritt 2 liefert `400`, weil der Nutzername bereits belegt ist (keine neue Ressource entsteht). Schritt 4 liefert jeweils Erfolgscodes, weil ein gültiger Token vorliegt und die Anfragen inhaltlich korrekt sind. Schritt 5 liefert `401`, weil die Signaturprüfung des manipulierten Tokens fehlschlägt - unabhängig davon, ob der Nutzer an sich berechtigt wäre.

## Grenzen

Dieser Ablauf prüft nur den "glücklichen" und einen manipulierten Pfad - Token-Ablauf (`expiresIn`) wurde hier nicht real abgewartet, sondern nur als Konzept erwähnt.
