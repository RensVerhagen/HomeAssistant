# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Home Assistant Version

Currently running **2025.12.1** (tracked in `.HA_VERSION`).

## Configuration Architecture

Configuration is split across multiple files included from `configuration.yaml`:

- `automations.yaml` — All UI-managed automations (52 automations, ~1600 lines)
- `config_files/backend_automations.yaml` — Backend automations (alarm logic, presence-based arming)
- `config_files/sensor.yaml` — Template sensors (appliance status, door timestamps)
- `config_files/groups.yaml` — Person groups (family: Rens + Nathasja, guests: Indy + Jamie)
- `config_files/cameras.yaml` — FFmpeg RTSP camera streams
- `config_files/alarm_control_panel.yaml` — Manual alarm panel config
- `config_files/customize.yaml` — Entity customizations
- `integrations/google_assistant.yaml` — Google Assistant exposed entities
- `integrations/notify.yaml` — Notification services (mobile apps + Telegram)
- `integrations/alert.yaml` — Persistent alert definitions
- `integrations/utility_meter.yaml` — Energy/gas tracking (daily + monthly)
- `integrations/sonoff.yaml` — Sonoff LAN config
- `scripts.yaml` — Script definitions
- `scenes.yaml` — Scene definitions

## Custom Integrations (via HACS in `custom_components/`)

- **Sonoff (SonoffLAN)** — Local control of Sonoff/eWeLink devices
- **Eufy Security** — Cameras and doorbell
- **Bosch Indego** — Lawn mower automation
- **Xiaomi Cloud Map Extractor** — Roborock vacuum map
- **WebRTC Camera** — Low-latency camera streams
- **Afvalwijzer** — Dutch waste collection schedule
- **HACS** — Custom integration package manager

## Public Repository Warning

This repository is **publicly available** at `https://github.com/RensVerhagen/HomeAssistant`. Every committed file is visible to anyone on the internet. Keep this in mind when editing any tracked file:

- Never commit household location data (coordinates, street address, postcode) — `home_latitude` and `home_longitude` must stay in `secrets.yaml`
- Never add real IP addresses, credentials, API keys, or alarm codes to any committed file
- Alarm timing and logic is fine to commit; the concern is physical location, not automation behavior
- Use `!secret key_name` for anything sensitive — `secrets.yaml` is git-ignored and safe

## Secrets

All sensitive values are stored in `secrets.yaml` (git-ignored). Reference them as `!secret key_name`. Never hardcode IPs, credentials, or tokens.

## Automations

- Automations managed via the HA UI are written to `automations.yaml`
- Backend/logic automations that shouldn't be edited via UI live in `config_files/backend_automations.yaml`
- Each automation requires a unique `id` field (used by HA for deduplication)
- Notifications use two channels: mobile app (via `notify.rens` / `notify.nathasja` / `notify.all_devices`) and Telegram (`notify.ha_thuis_group`, `notify.rens_telegram`)

## Language & Localization

- UI and TTS language: Dutch (`nl`)
- Entity names, automation aliases, and comments are in Dutch

## Deploying Changes

Changes take effect after reloading the relevant HA component (Automations, Scripts, etc.) or doing a full HA restart. There is no local test runner — validation is done by HA itself on reload.

## Python Scripts

`python_scripts/manage_token.py` manages long-lived API tokens for the Jukebox integration. It connects via WebSocket to `ws://homeassistant.local:8100/api/websocket` and writes tokens to `www/jukeboxtoken.key`.

## Git Workflow

- Branch: `master` (main branch, also used for PRs)
- Remote: `https://github.com/RensVerhagen/HomeAssistant`
- The `.gitignore` uses a whitelist approach — only explicitly allowed file types are tracked
