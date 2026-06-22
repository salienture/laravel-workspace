# Architecture

## Workspace layout

```
salienture-laravel-workspace/
├── app/                 # Clone your Laravel app(s) here — gitignored
│   └── .gitkeep         # Only committed file inside app/
├── docker/              # Compose stack + FrankenPHP image
├── docs/                # Human documentation
├── history/             # ADRs and session notes
├── scripts/             # Setup helpers
├── .devcontainer/       # VS Code / Cursor dev container
├── .cursor/rules/       # Cursor AI rules
├── .claude/             # Claude Code settings & commands
├── Makefile             # Primary dev interface
├── CLAUDE.md            # Claude Code project context
└── AGENTS.md            # Cross-agent instructions (Cursor, etc.)
```

## Design choices

1. **Generic workspace, separate app git** — `app/` is a gitignored container for any Laravel application. Each app is committed only to its own repository; the workspace never touches app history.

2. **Auto-detected app** — `scripts/setup.sh` scans `app/` for Laravel projects (`artisan` + `composer.json`). One app is selected automatically; multiple apps show a numbered picker. `APP_PATH`, `COMPOSE_PROJECT_NAME`, `DB_DATABASE`, and `DB_USERNAME` are all derived from the chosen app name.

3. **FrankenPHP in Docker** — Matches modern PHP deployment (Caddy, HTTP/2, optional workers) without replacing Laravel's `artisan` workflow. Runs PHP 8.5.

4. **Vite on host** — Faster HMR and simpler debugging. Laravel's `@vite()` directive handles dev/prod asset routing — no Caddy proxy needed.

5. **Redis for ephemeral state** — Sessions, cache, and queues use Redis in Docker; the app `.env` is patched by `scripts/patch-app-env.sh` to point at Docker service hostnames.

6. **Makefile as CLI** — Single entry point for humans and AI agents; wraps `docker compose` and `artisan`.

7. **Multi-workspace isolation** — `COMPOSE_PROJECT_NAME` namespaces all containers and volumes. Configurable port variables in `.env` allow multiple workspaces to run simultaneously without port conflicts.

## Application stack

- PHP 8.5, Laravel 13+
- Inertia.js + React / TypeScript + Tailwind CSS (typical setup)
- Pest (tests)

See the app's own `CLAUDE.md` or `composer.json` for app-specific details.
