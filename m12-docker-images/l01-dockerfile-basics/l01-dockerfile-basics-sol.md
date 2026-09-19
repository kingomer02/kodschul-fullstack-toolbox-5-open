# Lab 12.1 - Lösung: Dockerfile-Grundlagen

## Aufgabe 1: `greet.js`

```js
// sample-app/greet.js
const name = process.env.GREET_NAME || "world";
console.log(`Hello, ${name}!`);
```

## Aufgabe 2: Dockerfile

```dockerfile
# sample-app/Dockerfile
FROM node:24-alpine
WORKDIR /app
COPY greet.js .
ENV GREET_NAME=Docker
CMD ["node", "greet.js"]
```

## Aufgabe 3-4: Bauen und ausführen

```bash
docker build -t greet-sample sample-app/
docker run greet-sample
# Hello, Docker!
docker run -e GREET_NAME=Kurs greet-sample
# Hello, Kurs!
```

## Grenzen

`ENV` im Dockerfile setzt nur den Standardwert - `-e` beim `docker run` überschreibt ihn zur Laufzeit, ohne das Image neu bauen zu müssen.
