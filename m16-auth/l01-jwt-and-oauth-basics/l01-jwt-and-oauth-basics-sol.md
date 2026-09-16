# Lab 16.1 - Lösung: JWT und OAuth: Grundlagen

## Aufgabe 1: `server.ts`

Siehe vollständigen Code im Theorieteil (Lab 16.1, Abschnitt "Minimalbeispiel: Login und geschützte Route").

## Aufgabe 2: Login testen

```bash
curl -X POST http://localhost:3100/login \
  -H "Content-Type: application/json" -d '{"username": "sam"}'
# 200 { "token": "eyJhbGciOi..." }
```

## Aufgabe 3: Ohne Token

```bash
curl http://localhost:3100/profile
# 401 { "error": "missing token" }
```

## Aufgabe 4: Mit gültigem Token

```bash
curl http://localhost:3100/profile -H "Authorization: Bearer eyJhbGciOi..."
# 200 { "message": "you are authenticated" }
```

## Aufgabe 5: Manipulierter Token

```bash
curl http://localhost:3100/profile -H "Authorization: Bearer eyJhbGciOi...X"
# 401 { "error": "invalid token" }
```

## Grenzen

Der Token hat keine Rückruf-Möglichkeit ("Logout") - er bleibt bis zum Ablauf (`expiresIn`) gültig, selbst wenn der Server ihn "vergessen" möchte.
