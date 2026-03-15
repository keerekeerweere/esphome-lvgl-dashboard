# Repository Guidelines

## Project Structure & Module Organization
`index.yaml` is the main ESPHome entry point and composes `common.yaml`, `device.yaml`, and `layouts/main.yaml`. Keep hardware-specific settings in `device.yaml` and shared runtime features such as Wi-Fi, API, OTA, and diagnostics in `common.yaml`.

UI assets live under `layouts/`. Use `layouts/pages/` for room screens, `layouts/widgets/` for reusable LVGL components, `layouts/sensors/` for Home Assistant bindings, and `layouts/styles/`, `layouts/themes/`, and `layouts/fonts/` for presentation concerns. Store screenshots and static images in `images/`.

## Build, Test, and Development Commands
Create a local environment and install ESPHome:

```bash
python3.11 -m venv venv
source venv/bin/activate
pip install esphome
```

Validate configuration before committing:

```bash
esphome config index.yaml
```

Compile and flash locally:

```bash
esphome run index.yaml
```

Run the local dashboard for iterative work:

```bash
esphome dashboard .
```

## Coding Style & Naming Conventions
Use two-space YAML indentation and keep keys ordered in the style already used in nearby files. Prefer lowercase snake_case for file names, widget IDs, substitutions, and globals, for example `living_room.yaml` and `wifi_signal_strength`.

Keep page-specific entity bindings paired: when adding a control in `layouts/pages/<room>.yaml`, add or update the matching sensors in `layouts/sensors/<room>.yaml`. Reuse widgets with `!include` rather than duplicating LVGL blocks.

## Testing Guidelines
There is no separate unit test suite in this repository. The minimum check for every change is `esphome config index.yaml`; for hardware, also run a full compile or flash with `esphome run index.yaml`.

For UI changes, verify the affected page on-device and confirm touch behavior, state updates, and navigation. Include the changed room or widget name in your notes.

## Commit & Pull Request Guidelines
Recent commits use short, imperative subjects such as `Add light control panel and related scripts`. Follow that pattern and keep each commit focused on one feature or fix.

Pull requests should include a concise summary, impacted files or pages, any required `secrets.yaml` or Home Assistant entity changes, and screenshots for visible UI updates.

## Security & Configuration Tips
Never commit `secrets.yaml`, API keys, or Wi-Fi credentials. Keep local-only files in `.gitignore`, and use placeholder entity IDs in examples unless they are already part of the shared configuration.
