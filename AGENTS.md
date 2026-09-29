# Cristales Roca — Base44 dev notes

Static multi-page HTML/CSS/SCSS marketing site (no JS framework, no backend).
Pages live at the repo root (`index.html`) and in `pages/`. Styles are authored
in `scss/` and compiled to `css/style.css`.

## Running
`docker compose -f docker-compose.base44.yml up -d` serves the site on port 3000
with live reload. The image (`Dockerfile.base44`) bakes in `sass` + `live-server`;
the source is bind-mounted, so edits appear without rebuilding.

## Why a custom setup is needed
There is no `package.json`, build script, or server in the repo. A plain clone has
nothing listening on port 3000, so the import "failed to start". The compose file
adds the SCSS compile/watch + static file server.

## SCSS
`scss/main.scss` imports partials under `scss/assets/`. Dart Sass emits
`@import` deprecation warnings (not errors) — the build succeeds. Compiled output
is `css/style.css` (expanded style, no source map).

## Verify
- `curl -s -o /dev/null -w '%{http_code}' http://127.0.0.1:3000/` → 200
- Subpages: `http://127.0.0.1:3000/pages/<name>.html`
