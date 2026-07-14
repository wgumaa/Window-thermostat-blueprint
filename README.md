# Seasonal Window Thermostat Blueprint

Home Assistant automation blueprint for seasonal thermostat control based on one or more window sensors.

When any selected window opens, the thermostat is set to a configurable minimum temperature.  
When all selected windows are closed again, the thermostat is restored to the configured normal temperature for the current season using Home Assistant's default `sensor.season`.

## Features

- Supports one or more window sensors
- Uses a single window-open setback temperature
- Uses different normal temperatures for spring, summer, autumn, and winter
- Uses Home Assistant's built-in `sensor.season`
- Supports open and close delays
- Designed for easy reuse across multiple rooms

## Import into Home Assistant

### My Home Assistant import button

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/wgumaa/Window-thermostat-blueprint/main/blueprints/automation/wgumaa/window_thermostat_setback_and_restore.yaml)

### Manual import URL

```text
https://raw.githubusercontent.com/wgumaa/Window-thermostat-blueprint/main/blueprints/automation/wgumaa/window_thermostat_setback_and_restore.yaml
```

In Home Assistant:

1. Go to **Settings -> Automations & Scenes -> Blueprints**.
2. Click **Import Blueprint**.
3. Paste the raw URL above.
4. Click **Preview** and then **Import**.

## Blueprint location

```text
blueprints/automation/wgumaa/window_thermostat_setback_and_restore.yaml
```

## Inputs

- Window sensors
- Thermostat
- Window-open minimum temperature
- Spring normal temperature
- Summer normal temperature
- Autumn normal temperature
- Winter normal temperature
- Open delay
- Close delay

## Notes

- This blueprint uses `sensor.season` directly, so no season selector is needed.
- It is intended for thermostats that support `climate.set_temperature`.

## License

MIT
