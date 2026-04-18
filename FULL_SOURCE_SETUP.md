# Full Source Setup

This repo includes `ExpressLRS-full-source-custom.zip`, which is a backup of the full ExpressLRS source tree used during my custom ESP32-C3 Zero receiver build.

## What Is In The Zip

- ExpressLRS source tree
- My custom RX target change
- My custom hardware JSON files

The archive is here so I can return later and build again without repeating the whole setup process.

## Restore Steps

1. Download this repository or just `ExpressLRS-full-source-custom.zip`.
2. Extract the zip somewhere convenient.
3. Open the extracted `src` folder in VS Code with PlatformIO.
4. Confirm the custom target files are present.
5. Build the RX firmware.
6. Flash LittleFS.
7. Flash firmware.
8. Verify clean boot over serial.

## Build Commands

Run these from the extracted ExpressLRS `src` folder:

```powershell
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART --target uploadfs
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART --target upload
```

## Boot Check

After flashing:

- open serial at `420000` baud
- make sure there are no missing LittleFS file errors
- check for the ExpressLRS RX WiFi hotspot

## Important Reminder

The original boot issue was caused by the filesystem format mismatch.

This target needs:

`board_build.filesystem = littlefs`

If you flash firmware but skip `uploadfs`, or if the filesystem is built as SPIFFS instead of LittleFS, the receiver may fail to boot correctly.

## TX Firmware Later

This backup is for a custom RX target, not a TX target.

If you want TX firmware later:

1. Check official ExpressLRS TX targets first.
2. Review:
   - `targets/esp32-tx.ini`
   - `targets/esp32c3-tx.ini`
3. Use an official TX target if your hardware already exists.
4. If not, make a separate custom TX target instead of modifying this RX target.

## Quick Reminder

- RX target used here: `DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART`
- This repo does not currently include a custom TX target
