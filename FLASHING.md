# Reflashing Guide

## DIY ELRS ESP32-C3 Zero Receiver

Use this guide when you want to reflash the custom receiver firmware later.

## Every Time You Reflash

### Step 1

Open the project in VS Code:

`File -> Open Folder -> E:\expresslrsc3\ExpressLRS\src`

### Step 2

Open the terminal:

`Ctrl + ~`

### Step 3

Plug in the ESP32-C3 Zero by USB.

## Case A: Reflash Firmware Only

Use this if you only changed the binding phrase or other build flags and do not need to refresh the filesystem.

```powershell
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART --target upload
```

## Case B: Reflash Everything

Use this after a fresh clone, after major config changes, or if the board crashes on boot.

First flash the filesystem:

```powershell
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART --target uploadfs
```

Wait for `SUCCESS`, then flash firmware:

```powershell
pio run -e DIY_ESP32C3_Zero_SX1281_2400_RX_via_UART --target upload
```

## If Upload Gets Stuck At Connecting

1. Hold the `BOOT` button on the board.
2. Run the upload command.
3. Release the button when `Connecting...` appears.

## Verify It Worked

1. Wait about 60 seconds after flashing.
2. On your phone, connect to the receiver WiFi.
3. SSID: `ExpressLRS RX`
4. Password: `expresslrs`
5. Open: `http://10.0.0.1`

Expected result:

- The page should load successfully.
- The firmware target should show `DIY_ESP32C3_ZERO_SX1281_2400_RX`.

## Change Binding Phrase

Open `src/user_defines.txt` and edit:

```text
-DMY_BINDING_PHRASE="your-phrase-here"
```

Then do a full reflash:

- `uploadfs`
- `upload`

## Recommended Habit

If you are not sure whether only firmware is enough, do the full reflash sequence:

1. `uploadfs`
2. `upload`

That is the safest option for this custom target.
