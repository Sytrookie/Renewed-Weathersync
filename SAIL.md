# Renewed-Weathersync — Sail fork

This is **Sail’s fork** of [Renewed-Scripts/Renewed-Weathersync](https://github.com/Renewed-Scripts/Renewed-Weathersync), wired as a **git submodule** of the Sail monorepo.

| Field | Value |
|-------|--------|
| Sail fork | https://github.com/Sytrookie/Renewed-Weathersync |
| Upstream | https://github.com/Renewed-Scripts/Renewed-Weathersync |
| Monorepo path | `system_resources/[core]/Renewed-Weathersync` |
| License | GPL-3.0 (see `LICENSE`) |

## Why a fork (not upstream submodule)

1. Sail-owned patches (fxmanifest, config defaults, harness compat) commit and push here — not lost on `git submodule update`
2. Setup still clones/updates via submodule (see `tools/setup/Setup.ps1`)
3. Upstream can be merged deliberately without overwriting Sail work

## Monorepo wiring

- `server.cfg` / `server.cfg.example`: after `ox_lib`
  - `setr weather_disablecd true`
  - `ensure Renewed-Weathersync`
- Admin commands use `group.admin` (already present in Sail cfg)
- `sail_cas` asset harness pauses sync via `vSync:toggle` during studio capture

## Working on this resource

```bat
cd system_resources\[core]\Renewed-Weathersync
git checkout main
rem edit...
git add -A
git commit -m "your message"
git push origin main
cd ..\..\..
git add system_resources/[core]/Renewed-Weathersync
git commit -m "Bump Renewed-Weathersync submodule"
```

## Pulling upstream

```bat
cd system_resources\[core]\Renewed-Weathersync
git remote add upstream https://github.com/Renewed-Scripts/Renewed-Weathersync.git
rem (if not already present)
git fetch upstream
git merge upstream/main
rem resolve conflicts, re-check SAIL.md deltas, push origin main
```

## Do not

- Point the Sail submodule URL back at `Renewed-Scripts/Renewed-Weathersync`
- Force-push over fork history without coordinating monorepo pin updates
