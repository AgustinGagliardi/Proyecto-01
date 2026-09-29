# Cristales Roca — Base44 dev environment

## What this is
A static HTML/CSS/JS marketing site (no backend, no build step) for a windshield/glass business. Pages live at the repo root (`index.html`) and in `pages/`. Assets are in `resourse/` (note the spelling). Styles are pre-compiled to `css/style.css`; SCSS sources live in `scss/` but are not part of the build.

## Running it
- Served by `nginx:alpine` via `docker-compose.base44.yml` on host port 3000.
- Source is bind-mounted read-only; edits to HTML/CSS appear on browser refresh (no live-reload dev server — call `reload_preview` after changes if needed).
- A custom `nginx.base44.conf` sets `user root;` because the repo root dir is mode 0700 and the default `nginx` worker user cannot traverse it. Do not remove this override.

## No secrets
The app has no backend and needs no external credentials.

## Verification
- `curl -s -o /dev/null -w '%{http_code}' http://localhost:3000/` → 200
- Title should be "Cristales Roca".
