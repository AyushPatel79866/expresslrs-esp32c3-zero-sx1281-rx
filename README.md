# ExpressLRS ESP32-C3 Zero SX1281 RX

Custom ExpressLRS 4.0.0 receiver target for:

- Waveshare ESP32-C3 Zero
- Ebyte E28-2G4M27SX
- SX1281 2.4GHz radio
- CRSF UART output to a flight controller

This was my first time building and sharing a custom ExpressLRS target, and also my first time using AI to help me work through the setup, debugging, and flashing process.

## What This Repo Contains

- `src/targets/esp32-rx.ini.snippet`
- `src/hardware/2400/DIY_ESP32C3_Zero_SX1281_RX/config.json`
- `src/data/hardware.json`
- `src/user_defines.txt`
- `src/lib/OPTIONS/options.cpp.snippet`
- `ExpressLRS-full-source-custom.zip`
- `FULL_SOURCE_SETUP.md`

Use the `src/` files if you want to patch an existing ExpressLRS source tree.

Use `ExpressLRS-full-source-custom.zip` if you want the full source backup I used during this build.

## Build Base

- ExpressLRS version: `4.0.0`
- Branch used during this work: `master`
- Commit used during the original build session: `34a68884`
- Platform used: Windows 11 + VS Code + PlatformIO

## Hardware

- MCU: `Waveshare ESP32-C3 Zero`
- Radio module: `Ebyte E28-2G4M27SX`
- Radio chip: `SX1281`
- Output protocol: `CRSF`

## Pin Mapping

These values match the included `config.json` and `hardware.json`:

- `serial_rx` -> `GPIO20`
- `serial_tx` -> `GPIO21`
- `radio_busy` -> `GPIO3`
- `radio_dio1` -> `GPIO1`
- `radio_miso` -> `GPIO5`
- `radio_mosi` -> `GPIO4`
- `radio_nss` -> `GPIO7`
- `radio_rst` -> `GPIO2`
- `radio_sck` -> `GPIO6`
- `led` -> `GPIO10`
- `led_rgb` -> `GPIO10`

## Receiver Target Name

Build this receiver with:

`DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART`

## Important Fix

This target must use:

`board_build.filesystem = littlefs`

During the original setup, the receiver booted with missing `/littlefs/options.json` and `/littlefs/hardware.json` errors until the filesystem was built and flashed as LittleFS instead of SPIFFS.

There is also a custom name fallback fix included in this repo so the receiver does not keep showing `Unified RX` when using this custom non-`Unified_` target.

## Quick Start

1. Start from an ExpressLRS `4.0.0` source tree.
2. Add the env block from `src/targets/esp32-rx.ini.snippet` into `src/targets/esp32-rx.ini`.
3. Copy `src/hardware/2400/DIY_ESP32C3_Zero_SX1281_RX/config.json` into the matching location in the ExpressLRS tree.
4. Copy `src/data/hardware.json` into `src/data/` in the ExpressLRS tree.
5. Copy `src/user_defines.txt` values into your local `user_defines.txt`.
6. Apply the `src/lib/OPTIONS/options.cpp.snippet` fallback change if you want the custom device name to appear instead of `Unified RX`.
7. Build the firmware.
8. Flash the filesystem image first.
9. Flash the firmware image second.
10. Check the serial monitor at `420000` baud.

## Full Build Steps

From the ExpressLRS `src` directory:

```powershell
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART --target uploadfs
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART --target upload
```

## What To Check After Flashing

- Open a serial monitor at `420000` baud
- Confirm the receiver boots cleanly
- Confirm it no longer reports missing `hardware.json` or `options.json`
- Check for the ExpressLRS RX WiFi hotspot
- Confirm CRSF wiring and behavior on the flight controller side

## If You Come Back Later

Start with these files:

- `README.md`
- `FULL_SOURCE_SETUP.md`
- `src/targets/esp32-rx.ini.snippet`
- `src/hardware/2400/DIY_ESP32C3_Zero_SX1281_RX/config.json`
- `src/data/hardware.json`

If you want the exact working source tree I used, extract:

- `ExpressLRS-full-source-custom.zip`

## If You Want To Build RX Firmware Again

Follow this order:

1. Use the RX env `DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART`
2. Build
3. Run `uploadfs`
4. Run `upload`
5. Verify boot on serial at `420000`

Do not skip the filesystem flash if you are rebuilding from scratch.

## If You Want TX Firmware Later

This repository is for a custom RX target only.

Do not reuse this RX target directly for a transmitter build.

If you want TX firmware later:

1. Check whether your TX hardware already has an official ExpressLRS target.
2. Review upstream TX target files:
   - `targets/esp32-tx.ini`
   - `targets/esp32c3-tx.ini`
3. If your hardware already exists, use the official TX target.
4. If it does not exist, make a separate custom TX target and hardware config.

## Notes

- This repo is meant to make future rebuilds easier for me and for anyone using similar hardware.
- The `src/` files are the clean custom changes.
- The zip file is the backup copy of the full source tree used during this work.
