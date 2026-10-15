# Build and flash

> This repository starter contains **documentation only**. Copy the exact working firmware snapshots into the firmware folders first; do not attempt to flash placeholder files.

## Development environment observed

- ESP32-S3 N16R8
- Arduino IDE with Espressif's Arduino-ESP32 core (XInput USB experiments reported on 3.3.11)
- USB Mode: **USB-OTG / TinyUSB**
- USB CDC On Boot: **Disabled** (serial monitor via separate UART/upload port)
- Arduino libraries: `Adafruit MCP23X17` / `Adafruit_MCP23X17`, `Preferences`, `Wire` and built-in ESP32 USB support. Adafruit BusIO may be needed as a dependency.

Settings will vary depending on ESP32-S3 board variant; verify all before flashing. Exact tool versions and Arduino board-menu settings should be recorded from the final working build.

## Building

1. Install the ESP32 board package and Adafruit MCP23X17 library.
2. Open the `.ino` file from **one** selected firmware folder in the Arduino IDE. The sketch directory name must match the `.ino` basename.
3. Ensure the corresponding `.cpp` and `.h` files are in that same folder.
4. Flash via the existing programming/upload interface.
5. Connect the ESP32-S3 native USB data port to Windows using a known-good USB data cable.
6. Check the serial monitor (115200 baud where configured) and `joy.cpl`.

## Expected enumeration

- **DS4 mode**: PlayStation/DualShock-style USB HID device on supported games.
- **XInput mode**: Windows displays `Controller (XBOX 360 For Windows)` in the tested setup. The PS/Guide key should invoke Xbox Game Bar if Windows is configured to do so.

## Test carefully

Test button presses, D-pad, sticks and triggers before enabling high-power rumble. See [Testing](TESTING.md).

**Do not** simultaneously connect multiple conflicting 5V supplies. Unplug immediately if an actuator runs without a game command, overheats, or clicks excessively.
