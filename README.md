# Seasonal Window Thermostat Control

A Home Assistant automation blueprint for controlling a thermostat based on one or more window sensors and the current season.

When any selected window opens, the thermostat is set to a configurable minimum temperature. When all selected windows are closed again, the thermostat is restored to the configured normal temperature for the current season using Home Assistant’s built-in `sensor.season`.

## Overview

This blueprint is designed for rooms where opening a window should temporarily reduce heating demand, while still allowing a different normal target temperature for each season.

- Supports one or more window sensors for the same room
- Uses a single shared window-open setback temperature
- Uses separate normal temperatures for spring, summer, autumn, and winter
- Uses Home Assistant’s default `sensor.season` entity directly
- Supports open and close delays to avoid rapid toggling
- Designed to be reused across multiple rooms

Home Assistant blueprints are reusable automation templates that can be imported and then used to create automations from a shared YAML definition. [web:67][web:68]

## Features

- Multi-window support
- Seasonal normal temperature control
- Single configurable window-open minimum temperature
- Uses built-in `sensor.season`
- Open delay before setback is applied
- Close delay before normal temperature is restored
- Re-applies the correct temperature automatically if the season changes

## How it works

The blueprint follows this logic:

1. If any selected window opens and stays open for the configured delay, the thermostat is set to the configured window-open minimum temperature.
2. If all selected windows close and stay closed for the configured delay, the thermostat is set back to the configured normal temperature for the current season.
3. If the Home Assistant season changes, the blueprint re-applies the correct temperature based on whether any selected window is currently open.

The season is taken from Home Assistant’s built-in `sensor.season`, which reports `spring`, `summer`, `autumn`, or `winter`. [web:67]

## Inputs

| Input | Description |
|---|---|
| `window_sensors` | One or more window or door contact sensors for the room. |
| `thermostat` | Climate entity to control. |
| `window_open_temperature` | Temperature to set while any selected window is open. |
| `spring_normal_temp` | Normal target temperature used during spring. |
| `summer_normal_temp` | Normal target temperature used during summer. |
| `autumn_normal_temp` | Normal target temperature used during autumn. |
| `winter_normal_temp` | Normal target temperature used during winter. |
| `open_delay` | How long a window must stay open before the setback is applied. |
| `close_delay` | How long all windows must stay closed before the normal seasonal temperature is restored. |

## Installation

### Import into Home Assistant

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/wgumaa/Window-thermostat-blueprint/blob/main/blueprints/automation/Waleed%20Gumaa/window_thermostat_setback_and_restore.yaml)

### Import from a URL

Home Assistant supports importing a blueprint by URL through the Blueprints page. [web:67][web:143]

1. Copy this blueprint URL:

```text
https://github.com/wgumaa/Window-thermostat-blueprint/blob/main/blueprints/automation/Waleed%20Gumaa/window_thermostat_setback_and_restore.yaml
```

2. In Home Assistant, go to **Settings** -> **Automations & scenes** -> **Blueprints**.
3. Click **Import Blueprint**.
4. Paste the URL and import it.
5. Create an automation from the blueprint and fill in the required inputs.

### Manual raw URL

If GitHub import does not work, use this raw URL instead:

```text
https://raw.githubusercontent.com/wgumaa/Window-thermostat-blueprint/main/blueprints/automation/Waleed%20Gumaa/window_thermostat_setback_and_restore.yaml
```

### Manual installation

A blueprint can also be installed manually by placing the YAML file in Home Assistant’s blueprint folder. Local automation blueprints are typically stored under `/config/blueprints/automation/`. [web:63][web:146]

1. Save the YAML file to:

```text
/config/blueprints/automation/Waleed Gumaa/window_thermostat_setback_and_restore.yaml
```

2. Reload automations or restart Home Assistant if needed.
3. Create a new automation from the blueprint.

## Example use case

A bathroom thermostat should reduce heating when the bathroom window is opened, then restore the normal room temperature after the window is closed again.

Example seasonal values:

- Spring normal temperature: 22°C
- Summer normal temperature: 18°C
- Autumn normal temperature: 22°C
- Winter normal temperature: 23°C
- Window-open minimum temperature: 15°C

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

- This blueprint uses `sensor.season` directly, so no season selector is required.
- It is intended for thermostats that support `climate.set_temperature`.
- If you rename the blueprint folder, you must also update the GitHub import link and raw URL in this README.

## License

This project is licensed under the MIT License.
