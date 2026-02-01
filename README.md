# SliceMK ErgoDox Wireless Keymap

Custom ZMK keymap for the [SliceMK ErgoDox Wireless Lite](https://www.slicemk.com/products/ergodox-wireless-lite).

## Layers

| # | Name | Purpose |
|---|------|---------|
| 0 | BASE | QWERTY with home row mods |
| 1 | SYMB | Symbols and punctuation |
| 2 | PWR | Navigation, editing, sticky mods |
| 3 | NAV | Mouse movement and clicks |
| 4 | NMPAD | Numpad with operators |
| 5 | FN | Bluetooth, F13-F24, bootloader |

## Custom Behaviors

### `lt_pwr` - Layer Tap (Power)
Hold-tap optimized for the backspace/pwr layer key.
- **Tap**: Key press (e.g., BACKSPACE)
- **Hold**: Activate layer (e.g., PWR)
- **Settings**: `flavor=balanced`, `tapping-term=280ms`, `quick-tap=175ms`

### `hm` - Home Row Mods
Hold-tap for home row modifier keys (ASDF / JKL;).
- **Tap**: Letter key
- **Hold**: Modifier (Ctrl, Alt, GUI, Shift)
- **Settings**: `flavor=tap-preferred`, `tapping-term=200ms`, `require-prior-idle=150ms`
- **Prevents misfires** during fast typing with `tap-preferred` and idle requirement

### `td_shift_caps` - Tap Dance Shift/Caps
Tap dance on left shift key.
- **Single tap**: LEFT_SHIFT
- **Double tap**: CAPS_LOCK

### `arrow_left` / `arrow_right` - Word Jump Arrows
Hold-tap for arrow keys with word navigation.
- **Tap**: Single character movement (← / →)
- **Hold**: Word jump (Ctrl+← / Ctrl+→)
- **Settings**: `flavor=balanced`, `tapping-term=200ms`

## Layer Access

| Key | Tap | Hold |
|-----|-----|------|
| Top-right | BACKSPACE | PWR layer |
| Left thumb | SPACE | NAV layer |
| Left thumb | RETURN | PWR layer |
| Right thumb | BACKSPACE | SYMB layer |
| Inner columns | - | FN layer |
| Bottom thumb | ? | NMPAD layer |

## PWR Layer Shortcuts

| Key | Action |
|-----|--------|
| Ctrl+Z | Undo |
| Ctrl+Shift+Z | Redo |
| Ctrl+Shift+4 | Screenshot (macOS) |
| Tab / Shift+Tab | Indent/Outdent |
| Ctrl+A | Select All |
| Ctrl+X/C/V | Cut/Copy/Paste |
| Sticky mods | One-shot Ctrl/Shift/Alt/GUI |
| Arrow keys | Navigation |
| Ctrl+←/→ | Word jump |
| Home/End | Line start/end |
| Page Up/Down | Page navigation |

## Configuration

See `config/slicemk_ergodox_dongle.conf` for:
- `CONFIG_ZMK_MOUSE_DEFAULT_MOVE_VAL` - Mouse cursor speed

## Building

Push to GitHub to trigger automatic build. Download firmware from Actions artifacts.
