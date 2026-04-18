# Prebuilt Files

These files are for people who want to flash the custom receiver without rebuilding from source.

Included files:

- `full-flash.bin`
- `firmware.bin`
- `littlefs.bin`

## Easiest Option

Flash `full-flash.bin` at offset `0x0`.

That single file already includes:

- bootloader
- partitions
- boot app
- firmware
- LittleFS image

## Manual Two-File Option

1. Flash `littlefs.bin`
2. Flash `firmware.bin`

## Notes

- Target: `DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART`
- Board: `Waveshare ESP32-C3 Zero`
- Radio: `E28-2G4M27SX / SX1281`
- Filesystem must be LittleFS

## Important

If you use `full-flash.bin`, flash it to address `0x0`.

If someone only flashes `firmware.bin` and not `littlefs.bin`, the board may boot with missing file errors like:

- `/littlefs/hardware.json does not exist`
- `/littlefs/options.json does not exist`
