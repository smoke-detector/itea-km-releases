# Flashing ITEA-KM (beginner guide)

No coding or software install — flash straight from a web browser.

## What you need
- Your ESP32-S3 board.
- A **USB-C data cable** (some cheap cables are charge-only and will not work).
- A computer running **Chrome or Edge** (the web flasher needs a Chromium browser;
  Firefox and Safari will not work).

---

## Easy way — one file (recommended)

### 1. Download
From the latest release, download the single file named
**`itea-km-<version>-full.bin`** (e.g. `itea-km-0.3.3-full.bin`):
https://github.com/smoke-detector/itea-km-releases/releases/latest

### 2. Plug in
Connect the board's **COM** port to the computer with the data cable. If the board
has two USB-C ports, use the one **not** labeled "USB" for a first flash.

### 3. Open the web flasher
Go to **https://espressif.github.io/esptool-js/**, leave Baudrate at 921600, click
**Connect**, and pick the serial port that appears (often "USB Serial" or "CH343").

### 4. Add the one file at address 0
Click **Add File**, choose `itea-km-<version>-full.bin`, and set **Flash Address** to
**`0x0`**. Click **Program** and wait ~30-60 seconds.

### 5. Confirm
On your phone, join the Wi-Fi network **ITEA-KM** (password **ITEAdvisors**) and open
**http://100.65.0.1**. You should see the ITEA-KM page.

That's it. Later updates need no cable — use the web page:
**Device tab -> Firmware update**.

---

## Advanced way — four separate files

If you prefer, flash the individual files instead of the merged one. Add each at its
address:

| Flash Address | File |
|---|---|
| `0x0` | bootloader.bin |
| `0x8000` | partition-table.bin |
| `0x49000` | ota_data_initial.bin |
| `0x50000` | itea-km.bin |

---

## Troubleshooting
- **No port appears:** usually a charge-only cable (swap it) or a missing driver. This
  board uses a **CH343** USB-serial chip; Windows 11 normally installs it automatically,
  otherwise search for the "CH343 driver" from WCH.
- **"Failed to connect":** put the board in flash mode by hand — **hold BOOT, tap
  RESET, release BOOT**, then click Connect again.
- **It flashed but will not boot:** re-check the address(es) — a wrong offset is the
  most common mistake.
