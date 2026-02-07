# Copilot Instructions for ZMK Config Repository

## Project Overview
This is a ZMK firmware configuration repository for the [sliceMK ErgoDox Wireless Lite](https://www.slicemk.com/products/ergodox-wireless-lite). It uses [ZMK Firmware](https://zmk.dev) on Zephyr RTOS. Keymaps are created via the **sliceMK Web UI** and exported as JSON.

## Workflow
1. **Configure keymap** in [sliceMK web configurator](https://www.slicemk.com) → export JSON
2. **Push changes** to this repo → GitHub Actions builds firmware automatically
3. **Download artifacts** from the Actions run (`.uf2` firmware files)

No local toolchain required.

## Architecture

| Directory | Purpose |
|-----------|---------|
| `boards/shields/` | Custom shield definitions (overlay, keymap, Kconfig) |
| `config/west.yml` | West manifest, pins ZMK to `v0.3` |
| `build.yaml` | Build matrix for GitHub Actions |
| `zephyr/module.yml` | Declares repo as Zephyr module |

## Current Hardware
- **Board**: `raytac_mdbt50q_rx_green` (USB dongle receiver)
- **Shield**: `slicemk_ergodox_dongle`
- **Peripheral ID**: `40100`
- **Pairing**: Dongle-only (keyboard halves pair to dongle, not Bluetooth host)

## Adding Another Keyboard
1. Export JSON from sliceMK web UI (or create shield manually)
2. Add entry to `build.yaml`:
   ```yaml
   include:
     - board: <board_name>
       shield: <shield_name>
   ```
3. If custom shield needed, add to `boards/shields/<name>/`

## Keymap JSON Format (from sliceMK Web UI)
```json
{
  "Keyboard": "ergodox",
  "Board": "raytac_mdbt50q_rx_green",
  "Shield": "slicemk_ergodox_dongle",
  "Layers": [
    {
      "Name": "base",
      "Keys": [
        { "Behavior": "&kp", "Args": ["A"] },
        { "Behavior": "&mo", "Args": ["fn"] },
        { "Behavior": "&lt", "Args": ["pwr", "BACKSPACE"] },
        { "Behavior": "$custom", "Args": ["&gresc"] }
      ]
    }
  ],
  "Advanced": { "MouseMove": "1200", "BTParams": "6/399/900" }
}
```

### Key Behaviors
| Behavior | Usage | Example |
|----------|-------|---------|
| `&kp` | Key press | `["A"]`, `["LEFT_SHIFT"]` |
| `&mo` | Momentary layer | `["fn"]` |
| `&lt` | Layer-tap | `["layer", "KEY"]` |
| `&mt` | Mod-tap | `["LCTRL", "A"]` |
| `&trans` | Transparent | `[]` |
| `&none` | No action | `[]` |
| `$custom` | Raw behavior | `["&gresc"]` |

## Build Matrix (`build.yaml`)
```yaml
include:
  - board: raytac_mdbt50q_rx_green
    shield: slicemk_ergodox_dongle
    cmake-args: -DCONFIG_ZMK_STUDIO=y  # optional
    snippet: studio-rpc-usb-uart        # optional
```

## Adding a New Shield
1. Create `boards/shields/<name>/` with:
   - `<name>.overlay` - GPIO/matrix definition
   - `<name>.keymap` - Default keymap
   - `Kconfig.shield` + `Kconfig.defconfig`
2. Add to `build.yaml`

## External Dependencies
- ZMK: `https://github.com/slicemk/zmk` @ `main` (in `config/west.yml`)

## Important: sliceMK Fork Differences
The sliceMK ZMK fork differs from upstream ZMK:
- **Use `<dt-bindings/zmk/mouse.h>`** NOT `pointing.h` for mouse behaviors
- **Do NOT use** `ZMK_POINTING_DEFAULT_MOVE_VAL` define (not supported)
- **Do NOT use** `CONFIG_ZMK_MOUSE_DEFAULT_MOVE_VAL` Kconfig option (not supported)
- **Do NOT include** `<dt-bindings/zmk/rgb.h>` unless RGB is configured

## Code Maintenance Guidelines

### Before Removing Code
**ALWAYS** search for all usages before removing behaviors, macros, or definitions:

1. Use `grep_search` with the exact identifier name (not regex patterns that might miss matches)
2. Check for both `&macro_name` usage in keymaps AND references in behavior definitions
3. Verify no references exist in ALL layers before removal
4. Example search pattern: `"query": "lock_screen"` (not `"&lock_screen"` which might miss some matches)

### When Cleaning Up Unused Macros
- Search for macro name without `&` prefix to catch all references
- Check if used in layer bindings (e.g., `&lock_screen`)
- Check if used in behavior definitions (e.g., `bindings = <&lock_screen>`)
- Only remove after confirming zero matches

## SliceMK Offical Resources

- [Official sliceMK ZMK Documentation) (https://docs.slicemk.com/zmk/)