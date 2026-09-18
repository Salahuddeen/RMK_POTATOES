# RMK Charybdis Right-Side Bring-Up (Waveshare RP2040)

This repository is configured to test **only the right half** (including the PMW3610 trackball) on an RP2040 board.

## Current firmware scope

- Right-side matrix only (5x5 test matrix)
- PMW3610 trackball enabled
- Standalone bring-up profile (not split transport yet)

## Wiring

Use this mapping exactly, or update `/home/runner/work/RMK_POTATOES/RMK_POTATOES/keyboard.toml` to match your real wiring.

### Matrix wiring (right side)

- `row_pins = ["PIN_6", "PIN_7", "PIN_8", "PIN_9", "PIN_10"]`
- `col_pins = ["PIN_11", "PIN_12", "PIN_13", "PIN_14", "PIN_15"]`

Connect each row and column wire from your right-half matrix to the corresponding RP2040 GPIO pin.

### PMW3610 wiring

- `SCK  -> PIN_3`
- `SDIO -> PIN_2` (shared MOSI/MISO for PMW3610 half-duplex)
- `CS   -> PIN_4`
- `MOTION -> PIN_5`
- `VCC -> 3V3`
- `GND -> GND`

## Build and flash

1. Push changes to your branch.
2. In GitHub Actions, run **Build RMK firmware**.
3. Download the build artifact (`.uf2`) from the workflow run.
4. Put the Waveshare RP2040 into BOOTSEL mode (hold BOOT, press/reset USB connect).
5. A USB mass-storage device appears (RPI-RP2).
6. Copy the `.uf2` file to that drive.
7. Board reboots with the new firmware.

## Validation checklist

- Press keys on the right half and confirm key events are generated.
- Move the trackball and confirm pointer motion.
- If X/Y direction is wrong, set `invert_x`, `invert_y`, or `swap_xy` in `keyboard.toml` under `[[input_device.pmw3610]]`.

## Moving to full split later

When right-half bring-up is confirmed, migrate this config to split sections:

- matrix config into `[[split.peripheral]]` + `[split.peripheral.matrix]`
- PMW3610 config into `[[split.peripheral.input_device.pmw3610]]`
- add split transport config (`serial` or `ble`) for both halves
