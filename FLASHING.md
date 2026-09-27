# Flashing ITEA-KM (beginner guide)

No coding or software install — flash straight from a web browser.

## What you need
- Your ESP32-S3 board.
- A **USB-C data cable** (some cheap cables are charge-only and will not work).
- A computer running **Chrome or Edge** (the web flasher needs a Chromium browser;
  Firefox and Safari will not work).

## Step 1 — Download the firmware
From the latest release, download all **four** `.bin` files:
https://github.com/smoke-detector/itea-km-releases/releases/latest

- `bootloader.bin`
- `partition-table.bin`
- `ota_data_initial.bin`
- `itea-km.bin`

Put them in one folder (e.g. Downloads).

## Step 2 — Plug in the board
Connect the board's **COM** port to the computer with the data cable. If the board
has two USB-C ports, use the one **not** labeled "USB" for a first flash.

## Step 3 — Open the web flasher
Go to **https://espressif.github.io/esptool-js/**
1. Leave **Baudrate** at 921600.
2. Click **Connect**.
3. Pick the serial port that appears (often "USB Serial" or "CH343"), then connect.

## Step 4 — Add the four files at these addresses
Click **Add File** for each, and set the **Flash Address** exactly:

| Flash Address | File |
|---|---|
| `0x0` | bootloader.bin |
| `0x8000` | partition-table.bin |
| `0x49000` | ota_data_initial.bin |
| `0x50000` | itea-km.bin |

Click **Program** and wait ~30-60 seconds. The board reboots into the firmware.

## Step 5 — Confirm
On your phone, join the Wi-Fi network **ITEA-KM** (password **ITEAdvisors**) and open
**http://100.65.0.1**. You should see the ITEA-KM page.

## After the first flash
Later updates need no cable — use the web page: **Device tab -> Firmware update**,
either uploading an `itea-km.bin` or checking online.

## Troubleshooting
- **No port appears:** usually a charge-only cable (swap it) or a missing driver. This
  board uses a **CH343** USB-serial chip; Windows 11 normally installs it automatically,
  otherwise search for the "CH343 driver" from WCH.
- **"Failed to connect":** put the board in flash mode by hand — **hold BOOT, tap
  RESET, release BOOT**, then click Connect again.
- **It flashed but will not boot:** re-check the four addresses in Step 4.
