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
- Extra number row: traditional `1 2 3 4 5 6 7 8 9 0 - =` (Shift for `!@#$%^&*()_+`).
- Extra leftmost column: `Esc`, `Tab`, `Shift`, `Ctrl`.
- Extra rightmost key on the top letter row (right of `'`): `Backspace`.
- Trackball: mouse buttons on inner left thumbs; auto mouse layer on trackball motion. There are no `CpiInc` / `TrackballScroll` keycodes in RMK; CPI stays in toml.

## Changelog

### 2026-09-19

- Use RMK v0.9 and Miryoku.
- Switch Miryoku alphas from QWERTY to Colemak-DH.
- Keep a traditional number row with Shift-for-symbols.
- Left extra column: Esc, Tab, Shift, Ctrl.
- Right-of-quote key: Backspace.
- Restore reversed column pin order (`PIN_10` … `PIN_5`); that wiring was intentional.
