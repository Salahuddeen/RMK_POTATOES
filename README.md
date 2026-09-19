# RMK Charybdis Split Build (Dual RP2040 Zero)

This repository is configured for a **full split build** with two RP2040 Zero controllers:

- Left side: split central
- Right side: split peripheral + PMW3610 trackball

## Current firmware scope

- Split serial connection over `PIN_0` (half-duplex PIO)
- 5x6 matrix per side (total layout 5x12)
- Trackball enabled on right side only

Requested keymap and wiring choices are tracked in `REQUESTS.md`.

## Wiring

Use this mapping exactly, or update `keyboard.toml` to match your hardware.

### Split communication

- Central `PIN_0` <-> Peripheral `PIN_0`
- Configured as PIO half-duplex serial (`instance = "PIO0"`, same TX/RX pin)

### Keyboard matrix wiring (both sides, same)

- Columns (reverse order on purpose): `PIN_10`, `PIN_9`, `PIN_8`, `PIN_7`, `PIN_6`, `PIN_5`
- Rows: `PIN_11`, `PIN_12`, `PIN_13`, `PIN_14`, `PIN_15`
- Diode direction: `row2col = true`

### Trackball wiring (right side only)

- `MOTION -> PIN_1`
- `SCLK -> PIN_2`
- `SDIO -> PIN_3` (shared MOSI/MISO)
- `NCS -> PIN_4`
- `VCC -> 3V3`
- `GND -> GND`

## Build and flash

1. Push changes to your branch.
2. In GitHub Actions, run **Build RMK firmware**.
3. Download the workflow artifact(s) for the split build.
4. Flash the central firmware to the left RP2040 Zero (BOOTSEL -> copy UF2).
5. Flash the peripheral firmware to the right RP2040 Zero (BOOTSEL -> copy UF2).
6. Power both halves and verify key scan + trackball movement.

## Validation checklist

- Left-half keys register correctly.
- Right-half keys register correctly.
- Trackball movement is reported from right half.
- If cursor direction is inverted, adjust `invert_x`, `invert_y`, or `swap_xy` in `keyboard.toml`.
