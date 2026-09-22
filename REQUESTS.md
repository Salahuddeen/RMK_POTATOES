# Requested configuration

This is the source of truth for changes the owner asked for. Read it before editing `keyboard.toml`, `vial.json`, or wiring docs. Do not "correct" these choices unless a later entry here explicitly replaces them.

## Hardware (do not "fix")

- Split RP2040 Zero, serial half-duplex on `PIN_0` (PIO0, same TX/RX pin).
- 5x6 matrix per side, `row2col = true`.
- Rows: `PIN_11`, `PIN_12`, `PIN_13`, `PIN_14`, `PIN_15`.
- Columns are **reversed on purpose** on both halves:
  `PIN_10`, `PIN_9`, `PIN_8`, `PIN_7`, `PIN_6`, `PIN_5`.
  Do not restore left-to-right `PIN_5`…`PIN_10`.
- Right-side PMW3610 trackball: MOTION `PIN_1`, SCLK `PIN_2`, SDIO `PIN_3`, NCS `PIN_4`.

## Layout

- Firmware: RMK v0.9 `keyboard.toml` syntax (`[[keymap.layer]]`, `MT(key, mod, profile)`, RMK keycodes).
- Core: **Miryoku**, alphas **Colemak-DH**.
- Number row (persists on **every** layer): `Esc 1 2 3 4 5 6 7 8 9 0 Bspc`.
  Shift on `1`–`0` still gives `!@#$%^&*()`. `-` and `=` live on the Num/Sym layers.
- Extra leftmost column (letter rows): `Tab`, `Shift`, `Gui` (Win/Command), `Ctrl`.
- Extra rightmost column (letter rows): `Alt+1`, `Alt+2`, `TG(qwerty)` (guest QWERTY on/off; was Alt+3).
- Layer 7 `qwerty`: flat QWERTY, no home-row mods or Miryoku LTs. Same extras and number row as base.
- Trackball: mouse buttons on inner left thumbs; auto mouse layer on trackball motion.
- Trackball axes match stock ZMK (`swap_xy = true`, `invert_x = true`, `invert_y = true`) so rolling the ball up moves the cursor up, not diagonally.
- Trackball sensitivity is set in toml (`cpi = 800`), not by keys.
- Right thumbs (inner three): `LT(fun,LAlt)` / `LT(num,Enter)` / `LT(sym,Backspace)` (Vial LT6+LAlt, LT4+Enter, LT5+Bspc).

## Changelog

### 2026-09-19

- Use RMK v0.9 and Miryoku.
- Switch Miryoku alphas from QWERTY to Colemak-DH.
- Keep a traditional number row with Shift-for-symbols.
- Left extra column: Esc, Tab, Shift, Ctrl.
- Restore reversed column pin order (`PIN_10` … `PIN_5`); that wiring was intentional.
- Wrap the number row with Esc (left) and Backspace (right); shift `1`–`0` in by one; drop `-` `=` from that row.
- Number row is explicit on all layers (not transparent).
- Right extra column sends Alt+1 / Alt+2 / Alt+3 instead of empty User keys.
- Left of the ZXCDV row is Gui (Windows / macOS Command), not Shift.

### 2026-09-22

- Invert trackball Y (`invert_y = true`).
- Right thumbs: LT6/LAlt, LT4/Enter, LT5/Backspace.
- Guest QWERTY layer 7, toggled by `TG(qwerty)` on the key right of `/`.
- Trackball axes match stock ZMK: `swap_xy`, `invert_x`, and `invert_y` (replaces invert-Y-only; fixes diagonal-up).
