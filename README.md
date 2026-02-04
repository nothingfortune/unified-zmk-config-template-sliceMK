# SliceMK ErgoDox Wireless Keymap

Custom ZMK keymap for the [SliceMK ErgoDox Wireless Lite](https://www.slicemk.com/products/ergodox-wireless-lite).

## Layers

| # | Name | Purpose |
|---|------|---------|
| 0 | BASE | QWERTY with home row mods (GACS) |
| 1 | SYMB | Symbols and punctuation |
| 2 | PWR | Navigation, editing, sticky mods |
| 3 | NAV | Mouse movement and clicks |
| 4 | NMPAD | Numpad with F-keys and brightness |
| 5 | FN | Bluetooth, F13-F24, bootloader |

## Home Row Mods (GACS Layout)

Optimized for macOS - hold home row keys for modifiers:

**Left Hand (A S D F):**
| Key | Tap | Hold |
|-----|-----|------|
| A | a | ⌘ Cmd (LGUI) |
| S | s | ⌥ Option (LALT) |
| D | d | ⌃ Ctrl (LCTRL) |
| F | f | ⇧ Shift (LSHIFT) |

**Right Hand (J K L ;):**
| Key | Tap | Hold |
|-----|-----|------|
| J | j | ⇧ Shift (RSHIFT) |
| K | k | ⌃ Ctrl (RCTRL) |
| L | l | ⌥ Option (RALT) |
| ; | ; | ⌘ Cmd (RGUI) |

**Settings:**
- `flavor = balanced` - Better for chording
- `tapping-term-ms = 280` (200 for shift)
- `quick-tap-ms = 175` - Fast double-tap for repeating
- `require-prior-idle-ms = 150` - Prevents misfires during fast typing

## Custom Behaviors

### `bspc_word` - Backspace Word Delete
- **Tap**: Backspace (delete character)
- **Hold**: ⌥+Backspace (delete word on macOS)
- **Settings**: `tapping-term=300ms`

### `arrow_left` / `arrow_right` - Word Jump Arrows
- **Tap**: Single character movement (← / →)
- **Hold**: Word jump (Ctrl+← / Ctrl+→)

## Mouse Settings

Configured in keymap defines (before includes):
```c
#define ZMK_MOUSE_DEFAULT_MOVE_VAL 1800  // 3x default speed (600)
#define ZMK_MOUSE_DEFAULT_SCRL_VAL 20    // 2x default scroll (10)
```

**Acceleration:**
- Smooth ramp to max speed over 500ms
- `acceleration-exponent = 2` (quadratic curve)

## Layer Access

| Key | Tap | Hold |
|-----|-----|------|
| Top-right | BACKSPACE | Delete word (⌥+BS) |
| Left thumb | SPACE | NAV layer |
| Left thumb | RETURN | PWR layer |
| Right thumb | BACKSPACE | Delete word (⌥+BS) |
| Right thumb | SPACE | NAV layer |
| Inner columns | - | FN layer |
| Bottom thumb | ? | NMPAD layer |
| Bottom thumb | . | SYMB layer |

## Media Keys

Located on inner column keys:
- `C_PLAY_PAUSE` - Play/Pause
- `C_NEXT` - Next track
- `C_VOL_UP` / `C_VOL_DN` - Volume

## Building

Push to GitHub to trigger automatic build. Download `.uf2` firmware from Actions artifacts.
