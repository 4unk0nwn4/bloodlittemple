# Bloodlit Temple — Base44 Dev Notes

## What this is
A single-page static site (`index.html`) with images and a YouTube embed. No build step, no backend, no dependencies, no framework.

## How it runs
- `docker-compose.base44.yml` serves the repo root via `nginx:alpine` on host port 3000.
- Source is bind-mounted read-only at `/usr/share/nginx/html`, so edits to `index.html` or images are reflected on browser refresh (no rebuild needed).
- No live-reload dev server — plain static files. Call `reload_preview` after edits if the iframe doesn't refresh on its own.

## Known quirk
The repo root directory had `700` permissions, which blocked nginx's non-root worker. `chmod 755 .` was applied to fix this. If the 403 recurs after a fresh clone, re-run `chmod 755 .`.

## Verification
- `curl -s -o /dev/null -w "%{http_code}" http://localhost:3000/` → 200
- Page title: "Bloodlit Temple"
- Assets (`girl.jpg`, `artefact000.png`, `cvttrl_pixel.jpg`) all return 200.

## Secrets
None required. No external services.
