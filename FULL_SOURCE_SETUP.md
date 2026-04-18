# Full Source Backup

This repo also includes a backup zip of the full ExpressLRS source tree I used for this custom receiver target.

## Included

- Upstream ExpressLRS source tree
- My custom receiver target changes
- My hardware JSON files

## Backup File

- `ExpressLRS-full-source-custom.zip`

## Why This Is Here

I added this so I can come back later and build new firmware without repeating all of the setup work from scratch.

## Notes

- This is based on my local working source tree.
- The zip is meant as a practical backup, not as a replacement for the main ExpressLRS upstream project.
- The backup zip does not need PlatformIO build output to be useful, so temporary build folders may be excluded.

## Fast Restore

1. Download this repository or just the zip file.
2. Extract `ExpressLRS-full-source-custom.zip`.
3. Open the extracted `src` folder in VS Code with PlatformIO.
4. Build with:

```powershell
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART
```

5. Flash filesystem:

```powershell
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART --target uploadfs
```

6. Flash firmware:

```powershell
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART --target upload
```

## If You Want TX Firmware Later

This backup is centered around a custom RX target.

For future TX firmware work:

1. Check whether your transmitter hardware already exists in official ExpressLRS targets.
2. Review:
   - `targets/esp32-tx.ini`
   - `targets/esp32c3-tx.ini`
3. If your hardware is supported, build using the official TX target.
4. If your hardware is not supported, create a separate custom TX target instead of modifying this RX target.

Quick reminder:

- RX target used here: `DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART`
- This repo does not currently include a custom TX target
