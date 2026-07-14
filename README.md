# Seasonal Window Thermostat Control

A Home Assistant automation blueprint for controlling a thermostat based on one or more window sensors and the current season.

When any selected window opens, the thermostat is set to a configurable minimum temperature. When all selected windows are closed again, the thermostat is restored to the configured normal temperature for the current season using Home Assistant's built-in `sensor.season`.

## Overview

This blueprint is intended for rooms where opening a window should temporarily reduce heating demand while still allowing different normal temperatures for each season.

### What it does

- Monitors one or more window sensors
- Applies a setback temperature when any selected window is open
- Restores the seasonal normal temperature when all selected windows are closed
- Uses Home Assistant's built-in `sensor.season`
- Supports configurable open and close delays
- Re-applies the correct target temperature if the season changes

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
| `open_delay` | How long a window must stay open before setback is applied |
| `close_delay` | How long all windows must stay closed before normal temperature is restored |

## How it works

1. If any selected window opens and stays open for the configured delay, the thermostat is set to the window-open minimum temperature.
2. If all selected windows close and remain closed for the configured delay, the thermostat is restored to the configured normal temperature for the current season.
3. If the season changes, the blueprint re-checks the situation and applies the correct temperature again.

## Installation

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/wgumaa/Window-thermostat-blueprint/blob/main/blueprints/automation/Waleed%20Gumaa/window_thermostat_setback_and_restore.yaml)

### Import from GitHub

Copy this blueprint URL:

```text
https://github.com/wgumaa/Window-thermostat-blueprint/blob/main/blueprints/automation/Waleed%20Gumaa/window_thermostat_setback_and_restore.yaml
```

Then in Home Assistant:

1. Go to **Settings** -> **Automations & scenes** -> **Blueprints**.
2. Click **Import Blueprint**.
3. Paste the URL above.
4. Click **Preview** and then import it.

### Manual raw URL

If needed, try this raw URL:

```text
https://raw.githubusercontent.com/wgumaa/Window-thermostat-blueprint/main/blueprints/automation/Waleed%20Gumaa/window_thermostat_setback_and_restore.yaml
```

### Manual installation

You can also install the blueprint manually by placing the YAML file in your Home Assistant blueprint folder.

Save the file here:

```text
/config/blueprints/automation/Waleed Gumaa/window_thermostat_setback_and_restore.yaml
```

Then reload automations or restart Home Assistant.

## Example use case

A bathroom thermostat should reduce heating when the bathroom window is opened, then restore the room's normal seasonal temperature when the window is closed again.

Example values:

- Spring: 22°C
- Summer: 18°C
- Autumn: 22°C
- Winter: 23°C
- Window-open temperature: 15°C

## Repository contents

```text
.
├── README.md
└── blueprints/
    └── automation/
        └── Waleed Gumaa/
            └── window_thermostat_setback_and_restore.yaml
```

## Notes

- This blueprint uses `sensor.season` directly.
- It is intended for thermostats that support `climate.set_temperature`.
- If you rename the folder or YAML file, update the import links in this README.

## License

MIT
