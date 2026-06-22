# Changelog

All notable changes to this **workspace** (not the Laravel app in `app/`) are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

## [1.0.0] — 2026-06-22

### Added

- Generic workspace — clone any Laravel app into `app/`, auto-detected by `make setup`
- `scripts/setup.sh`: scans `app/` for Laravel projects; auto-selects single app, interactive picker for multiple
- `app/` gitignored container directory; only `app/.gitkeep` is committed; each app lives in its own repo
- FrankenPHP (PHP 8.5) + MariaDB 11.4 + Redis 7 + Mailpit + phpMyAdmin Docker stack
- Optional queue and scheduler services (`workers` compose profile)
- Makefile targets: `init`, `setup`, `reconfigure`, `artisan`, `composer`, `test`, `pint`, `tinker`, `dump`, `restore`, `queue-restart`, `build-assets`, `fresh`, `seed`, `shell`, `mysql`, `redis-cli`, `logs`, `optimize`, `cache-clear`, `destroy`
- `COMPOSE_PROJECT_NAME`, `DB_DATABASE`, `DB_USERNAME` derived from app name — multiple workspaces never collide
- Port variables in `.env` for running multiple workspaces simultaneously
- Xdebug support via `INSTALL_XDEBUG=true` build arg and `XDEBUG_MODE` runtime env
- `make destroy` confirmation prompt to prevent accidental data loss
- `make dump` / `make restore` for database backup and restore
- Dev container configuration (VS Code / Cursor)
- Claude Code (`CLAUDE.md`, `.claude/`) and Cursor (`.cursor/rules/`, `AGENTS.md`) AI assistant configuration
- Built by [Salienture](https://salienture.com)
