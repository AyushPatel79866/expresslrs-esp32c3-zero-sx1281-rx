# ExpressLRS ESP32-C3 Zero SX1281 Receiver

Custom ExpressLRS receiver target for:

- Waveshare ESP32-C3 Zero
- Ebyte E28-2G4M27SX
- SX1281 2.4GHz receiver
- CRSF UART output to a flight controller

This was my first time putting together and sharing something like this, and also my first time using AI to help me work through the setup and debugging.

## Status

- Based on ExpressLRS 4.0.0
- Built and flashed successfully with PlatformIO on Windows
- Uses LittleFS for the filesystem image

## Included Files

- `src/targets/esp32-rx.ini.snippet`
- `src/hardware/2400/DIY_ESP32C3_Zero_SX1281_RX/config.json`
- `src/data/hardware.json`

## Wiring

- `SCK` -> `GPIO6`
- `MISO` -> `GPIO5`
- `MOSI` -> `GPIO4`
- `NSS/CS` -> `GPIO7`
- `BUSY` -> `GPIO3`
- `DIO1` -> `GPIO1`
- `RST` -> `GPIO2`
- `CRSF RX` -> `GPIO20`
- `CRSF TX` -> `GPIO21`

## How To Use

1. Start with an ExpressLRS 4.0.0 source tree.
2. Add the env block from `src/targets/esp32-rx.ini.snippet` to `src/targets/esp32-rx.ini`.
3. Copy `config.json` into `src/hardware/2400/DIY_ESP32C3_Zero_SX1281_RX/`.
4. Copy `hardware.json` into `src/data/`.
5. Build with:

```powershell
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART
```

6. Flash filesystem:

```powershell
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART --target uploadfs
```

7. Flash firmware:

```powershell
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART --target upload
```

## Notes

- `board_build.filesystem = littlefs` is required for this target.
- The filesystem image must be flashed before or along with firmware so `hardware.json` is available at boot.
