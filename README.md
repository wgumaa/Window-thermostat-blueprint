# Seasonal Window Thermostat Control

A Home Assistant automation blueprint for controlling a thermostat based on one or more window sensors and the current season.

When any selected window opens, the thermostat is set to a configurable minimum temperature. When all selected windows are closed again, the thermostat is restored to the configured normal temperature for the current season using Home Assistant's built-in `sensor.season`.

## Overview

This blueprint is designed for rooms where opening a window should temporarily reduce heating demand while still allowing different normal temperatures for each season.

### Features

- Supports one or more window sensors for the same room
- Sets the thermostat to a configurable minimum temperature when a window is open
- Restores the normal target temperature when all windows are closed
- Uses different normal temperatures for spring, summer, autumn, and winter
- Uses Home Assistant's built-in `sensor.season`
- Supports open and close delays
- Re-applies the correct temperature if the season changes

## How it works

1. If any selected window opens and stays open for the configured delay, the thermostat is set to the configured window-open temperature.
2. If all selected windows close and stay closed for the configured delay, the thermostat is restored to the configured seasonal normal temperature.
3. If the season changes, the blueprint applies the correct temperature again based on whether any window is currently open.

## Inputs

| Input | Description |
|---|---|
| `window_sensors` | One or more window or door contact sensors for the room |
| `thermostat` | Climate entity to control |
| `window_open_temperature` | Temperature to set while any selected window is open |
| `spring_normal_temp` | Normal target temperature for spring |
| `summer_normal_temp` | Normal target temperature for summer |
| `autumn_normal_temp` | Normal target temperature for autumn |
| `winter_normal_temp` | Normal target temperature for winter |
| `open_delay` | How long a window must stay open before the setback is applied |
| `close_delay` | How long all windows must stay closed before the normal temperature is restored |

## Installation

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/wgumaa/Window-thermostat-blueprint/blob/main/window_thermostat_setback_and_restore.yaml)

### Import from a URL

1. Copy this blueprint URL:

```text
https://github.com/wgumaa/Window-thermostat-blueprint/blob/main/window_thermostat_setback_and_restore.yaml
```

2. In Home Assistant, go to **Settings** -> **Automations & scenes** -> **Blueprints**.
3. Click **Import Blueprint**.
4. Paste the URL above.
5. Click **Preview** and import it.
6. Create a new automation from the blueprint.

### Manual installation

You can also install the blueprint manually by placing the YAML file in your Home Assistant blueprint folder. Home Assistant blueprints are commonly stored under `/config/blueprints/automation/<your_folder>/your_blueprint.yaml`. [web:146][web:149]

Save the file here, for example:

```text
/config/blueprints/automation/wgumaa/window_thermostat_setback_and_restore.yaml
```

Then reload automations or restart Home Assistant if needed.

## Example use case

A bathroom thermostat should reduce heating when the bathroom window is opened, then restore the room's normal seasonal temperature once the window is closed again.

Example values:

- Spring normal temperature: 22°C
- Summer normal temperature: 18°C
- Autumn normal temperature: 22°C
- Winter normal temperature: 23°C
- Window-open temperature: 15°C

## Repository contents

```text
.
├── README.md
└── window_thermostat_setback_and_restore.yaml
```

## Notes

- This blueprint uses `sensor.season` directly, so no season selector is required.
- It is intended for thermostats that support `climate.set_temperature`.
- If you move or rename the YAML file later, update the import link in this README.

## License

MIT
