# ITEA-KM User Manual

ITEA-KM is a small USB and Bluetooth keyboard/mouse. It types stored text
("paste profiles") into any computer, lets you control that computer's keyboard
and mouse from your phone, and can keep it awake. The computer needs no drivers
or software: it just sees a keyboard and a mouse.

Firmware 0.2.0.

---

## 1. The device

| Part | What it does |
|---|---|
| **USB** port (USB-C) | Connect to the computer you want to type into |
| **COM** port (USB-C) | Power, firmware updates and diagnostics |
| **BOOT** button | Paste, show network info, reset Wi-Fi (see section 6) |
| **RST** button | Restart. Never erases anything |
| RGB LED | Light show / button feedback (section 8) |

For normal use, plug only the **USB** port into the target computer. It powers
the device and carries the keyboard and mouse.

---

## 2. First setup

1. Plug the **USB** port into a computer (or any USB power source).
2. On your phone or laptop, join the Wi-Fi network **ITEA-KM**.
   The default password is provided separately by your administrator.
3. Open **http://100.65.0.1** in a browser.

The hotspot gives your phone an address but no internet route, so the phone
keeps using mobile data. If your phone asks whether to stay connected to a
network without internet, choose **Stay connected** / **Use without internet**.

### Join a local Wi-Fi network (optional)

1. Open the **Wi-Fi** tab, tap **Scan**, pick the network and enter its password.
2. Tap **Join**. Reconnect your phone/laptop to that same network.
3. Open **http://itea-km.local** or the IP address the device got.

If the device cannot join within 30 seconds (wrong password, network not
found), it brings the **ITEA-KM** hotspot back. A network is only saved after
a successful connection.

---

## 3. Paste profiles (Paste tab)

A profile is a named block of text the device types for you: a login, a
switch configuration, a set of commands.

- Up to **10 profiles**, each up to **65,536 bytes**.
- **Save** stores the profile. **Delete** removes it.
- **Set active** marks the profile the BOOT button types (★).
  **Deactivate** leaves no active profile, so a short BOOT press types nothing.
- **Paste now** types the text in the editor. Choose a **start after** delay
  (0–10 s) if this page is open on the same computer, so you have time to click
  into the target field.
- **Stop** stops typing immediately.
- **Typing speed**: delay between characters (0–1000 ms, default 20). Increase
  it if a switch console, login screen or slow system drops characters.

### Special keys in profiles

A new line presses **Enter**, a tab character presses **Tab**. Braces insert keys:

| Type this | To press |
|---|---|
| `{ENTER}` `{TAB}` `{ESC}` `{SPACE}` | Enter, Tab, Escape, Space |
| `{BACKSPACE}` `{DEL}` `{INSERT}` | Backspace, Delete, Insert |
| `{UP}` `{DOWN}` `{LEFT}` `{RIGHT}` | Arrow keys |
| `{HOME}` `{END}` `{PGUP}` `{PGDN}` | Navigation keys |
| `{F1}` … `{F24}` | Function keys |
| `{CAPSLOCK}` `{PRINTSCREEN}` `{MENU}` `{WIN}` | Other keys |
| `{CTRL+ALT+DEL}` `{WIN+R}` `{ALT+F4}` `{SHIFT+TAB}` `{CTRL+c}` | Key combinations |
| `{DELAY 1500}` | Wait 1.5 seconds (up to 60000 ms) |
| `{{` | A literal `{` |

Modifiers: CTRL, SHIFT, ALT, WIN (also RCTRL, RSHIFT, RALT/ALTGR, RWIN).
Unknown tokens are typed as written.

Example, log in to a device and save:

```
admin{TAB}{DELAY 300}MyPassword{ENTER}{DELAY 2000}write memory{ENTER}
```

The device assumes a **US keyboard layout** on the target computer. Characters
outside standard ASCII are skipped. Caps Lock on the target is detected and
corrected automatically.

---

## 4. Remote control (Remote tab)

Use your phone as the computer's mouse and keyboard.

**Trackpad**
- Drag to move the pointer. Adjust **Speed** with the slider.
- Tap to click. Two-finger tap to right-click.
- Two-finger drag to scroll.
- Tap, then touch and hold again to drag (hold the left button). Lift to release.
- **Left / Middle / Right** buttons, and **Hold left** to lock the left button.

**Keyboard**
- Tap the text box and type; keys are sent live.
- **Ctrl / Alt / Shift / Win** apply to the next key.
- Buttons for Esc, Tab, Enter, arrows, Ctrl+Alt+Del, Win+R, Win+L, Alt+Tab,
  copy/paste and more. Function keys F1–F12 are under **Function keys**.
- **Combination** box: send anything like `CTRL+SHIFT+ESC`.

If the page is closed or the phone locks, any held mouse button is released.

---

## 5. Keep awake (Jiggle tab)

Stops the connected computer from locking or going to sleep.

- **Mouse nudge**: moves the pointer one pixel and back.
- **Silent key (F15)**: presses F15, a real function key that operating systems
  count as activity but almost no software reacts to.
- **Both**.
- Choose how often (5–3600 seconds) and tap **Save**; tick **On** to start.

The jiggler never types text and pauses while a paste is running. It is off by
default and remembers its setting after a restart.

---

## 6. The BOOT button

| Press | Result |
|---|---|
| **Short press** | Types the active profile. The LED flashes blue. Pressing while typing stops it |
| **Hold 5 seconds** | Immediately types the device's network information (no Enter), e.g. `ITEA-KM 192.168.1.50/24 SSID OfficeWiFi STA-MAC … AP-MAC …` |
| **Hold 15 seconds** | Types `RESETTING WI-FI …`, then forgets the Wi-Fi network, sets the IP back to DHCP, restores the default hotspot password and starts the ITEA-KM hotspot. Profiles are kept |

While BOOT is held the LED shows the time: green brightens from 0 to 7 s,
it goes dark for a second, red brightens from 8 to 15 s, then it goes dark as
the Wi-Fi reset starts. You do not need to release the button for the 5 s and
15 s actions.

In hotspot mode the 5-second line includes the hotspot password only while it
is the default. A changed password is never typed; it shows
`PW has been changed`.

Tip: open Notepad on the connected computer before holding BOOT, so the typed
information lands somewhere harmless.

**RST** restarts the device and never erases settings. Holding **BOOT** while
pressing **RST** enters firmware-download mode (for updates over the COM port).

---

## 7. Wi-Fi settings (Wi-Fi tab)

- **Status**: current network, IP address, netmask, gateway, signal and MAC addresses.
- **Join a network**: see section 2.
- **IP settings**: DHCP (automatic) or Static (IP, netmask, gateway, DNS).
  If a static address makes the device unreachable, hold BOOT 15 seconds.
- **Hotspot**: the name is always **ITEA-KM**. You can change its password
  (8–63 characters) or **Restore default**. A changed password is never shown
  or typed again; if it is forgotten, restore the default (Restore default,
  Forget network, or hold BOOT 15 seconds).
- **Forget network**: clears the saved network, IP settings and hotspot
  password and returns to the hotspot. Profiles are kept.

---

## 8. LED (LED tab)

- **Light show**: Solid, Rainbow, Breathe, Heartbeat, Police, Fire, Party, Ocean.
- **Color** (for Solid, Breathe and Heartbeat), **Brightness** (0% = off) and **Speed**.
- Settings are saved and survive a restart.

---

## 9. Bluetooth (Device tab)

The device can also be a Bluetooth keyboard and mouse named
**Wireless Keyboard**. It is off by default.

1. Tick **Bluetooth on**.
2. Tap **Pair new device**. Pairing is open for 2 minutes.
3. On the computer, tablet or phone, add a Bluetooth device and choose
   **Wireless Keyboard**. No PIN is needed.

Outside the pairing window new devices are refused, and already paired devices
reconnect by themselves. **Forget paired devices** removes them all.

Pastes, the BOOT button, the Remote tab and the jiggler go to every connected
computer at the same time: USB and Bluetooth.

---

## 10. Device tab

- Firmware version, uptime, memory, Caps Lock state of the connected computer.
- **Restart**.
- **Factory reset**: erases everything (Wi-Fi, IP settings, hotspot password,
  profiles, typing speed, LED, jiggler, Bluetooth pairings) and starts the hotspot.

---

## 11. Troubleshooting

| Problem | Try |
|---|---|
| Page does not load on the hotspot | Use `http://100.65.0.1` (not https). Make sure the phone is still on ITEA-KM |
| `itea-km.local` does not work | Use the IP address. Hold BOOT 5 s with Notepad open to see it |
| Nothing is typed | Header must show **USB connected** or **BT connected**. Check a profile is active (★) |
| Characters are missing or wrong | Raise the typing speed delay. Check the computer uses a US keyboard layout |
| Symbols like `@ " # \` come out wrong | The computer's keyboard layout is not US |
| Can't reach the device after changing IP | Hold BOOT 15 seconds, then rejoin the ITEA-KM hotspot |
| Forgot the hotspot password | Hold BOOT 15 seconds to restore the default |
| Bluetooth device won't pair | Tap **Pair new device** again; pairing is only open for 2 minutes |

---

## 12. Safety notes

- The web page has no login. Anyone on the same Wi-Fi network (or the ITEA-KM
  hotspot) can use it to type into the connected computer. Change the hotspot
  password and only join trusted networks.
- Profiles are stored unencrypted on the device. Treat a device that holds
  passwords like a written password.
- Unplug the device when you are done with a computer.
