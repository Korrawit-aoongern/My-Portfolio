# Docker usage — vite-project

This folder contains a multi-stage Dockerfile to build the Vite app and serve the generated static files with nginx.

Files added/updated:

- `Dockerfile` and `dockerfile` — multi-stage build (Node builder + nginx runtime)
- `nginx.conf` — nginx config with SPA routing (fallback to index.html)
- `.dockerignore` — keeps build context small (ignores node_modules, dist, etc.)

Build and run locally (from the `vite-project` directory):

Powershell / Windows:

```
docker build -t my-portfolio:latest .
docker run -d -p 8080:80 --name my-portfolio my-portfolio:latest

# then open http://localhost:8080
```

Notes:
- The build stage runs `npm run build` and copies the `dist/` output into nginx's serving directory.
- If you already have a Dockerfile with a different name, use `docker build -f path/to/Dockerfile ...` or remove the old one.
