# Home Assistant Configuration

My personal [Home Assistant](https://www.home-assistant.io/) configuration.

## Structure

Configuration is split into focused files included from `configuration.yaml`:

| File | Purpose |
|------|---------|
| `automations.yaml` | UI-managed automations |
| `config_files/backend_automations.yaml` | Backend automations (alarm logic, presence-based arming) |
| `config_files/sensor.yaml` | Template sensors (appliance status, door timestamps) |
| `config_files/groups.yaml` | Person groups (family + guests) |
| `config_files/cameras.yaml` | FFmpeg RTSP camera streams |
| `config_files/alarm_control_panel.yaml` | Alarm panel configuration |
| `config_files/customize.yaml` | Entity customizations |
| `integrations/google_assistant.yaml` | Google Assistant exposed entities |
| `integrations/notify.yaml` | Notification services |
| `integrations/alert.yaml` | Persistent alert definitions |
| `integrations/utility_meter.yaml` | Energy & gas tracking (daily + monthly) |
| `integrations/sonoff.yaml` | Sonoff LAN configuration |
| `scripts.yaml` | Script definitions |
| `scenes.yaml` | Scene definitions |

## Custom Integrations (HACS)

- **[SonoffLAN](https://github.com/AlexxIT/SonoffLAN)** — Local control of Sonoff/eWeLink devices
- **[Eufy Security](https://github.com/fuatakgun/eufy_security)** — Cameras and doorbell
- **[Bosch Indego](https://github.com/eavanvalkenburg/pyindego)** — Lawn mower automation
- **[Xiaomi Cloud Map Extractor](https://github.com/PiotrMachowski/Home-Assistant-custom-components-Xiaomi-Cloud-Map-Extractor)** — Roborock vacuum map
- **[WebRTC Camera](https://github.com/AlexxIT/WebRTC)** — Low-latency camera streams
- **[Afvalwijzer](https://github.com/xirixiz/homeassistant-afvalwijzer)** — Dutch waste collection schedule
- **[HACS](https://hacs.xyz/)** — Custom integration package manager

## Language

UI, TTS, and automation names are in Dutch (`nl`).
