# PlayStation Portal Controller Mod

**A DIY ESP32-S3 USB controller built from original PlayStation Portal controller hardware, with experimental DualShock 4 and native Xbox 360/XInput modes.**

> **Unofficial hardware/firmware project.** Not affiliated with, sponsored by, or endorsed by Sony, PlayStation, Microsoft, or Xbox. The project reuses original controller components; it does **not** turn an intact Portal into a complete gaming handheld by itself.

<!-- Add an image: ![Modified Portal controller](media/portal-hero.jpg) -->

## The idea

I wanted to reuse the original controls of a PlayStation Portal in a custom Windows handheld / wired USB controller setup, without having to run Steam Input or manually remap every non-Steam game.

The project started by reverse-engineering the Portal's physical inputs. It evolved into a working ESP32-S3-based controller that speaks two different USB controller protocols **in separate firmware builds**:

| Mode | What it emulates | Observed status |
|---|---|---|
| **DS4** | Wired DualShock 4-style HID controller | Experimental v1.0 RC1 snapshot; native PlayStation prompts and rumble observed in Battlefield |
| **XInput** | Wired Xbox 360-style USB controller | Working development build; Xbox button prompts and native rumble tested in Battlefield 6 and Zenless Zone Zero |

Both builds share hardware, calibration ideas, and haptic driver logic. A runtime mode switch has **not** been implemented yet; switching currently requires flashing a different build.

## Highlights

- Original Portal D-pad, face buttons, shoulder buttons, analog sticks, analog triggers, L3/R3, PS, Start and Select
- **Native USB XInput** on ESP32-S3 using a custom TinyUSB vendor-class driver — no ViGEm or Steam Input required for the Windows games tested
- DS4-style USB HID mode with selected feature reports (e.g. `0x02`, `0x12`, `0xA3`)
- USB rumble/output report handling through a DRV8833 and the original Portal haptic actuators
- RGB lightbar and local Mute LED behavior
- Saved calibration and LED preferences via ESP32 NVS
- Native Xbox Guide button launches Xbox Game Bar on the tested Windows setup

## Architecture

~~~mermaid
flowchart TD
    A[Original Portal controller controls] --> B[ESP32-S3 input and calibration]
    E[MCP23017 GPIO expander] --> B
    B --> C{Flash selected firmware}
    C --> D[DS4 HID USB mode]
    C --> X[Xbox 360 XInput USB mode]
    D --> W[Windows / compatible games]
    X --> W
    W --> R[USB rumble output]
    R --> H[DRV8833 haptic driver]
    H --> M[Original Portal actuators]
~~~

See [Architecture](docs/ARCHITECTURE.md) and [Hardware wiring](docs/WIRING.md).

## Hardware

- ESP32-S3 module (developed on **N16R8**)
- Original PlayStation Portal controller halves / control flex cables
- MCP23017 I²C GPIO expander
- DRV8833 dual H-bridge motor driver
- Original Portal haptic actuators
- USB-C breakout with USB D−/D+, VBUS and GND wired to the ESP32-S3 native USB connection
- Other connectors, flex breakouts and wiring as required

**Hardware caution:** These are the pin assignments from a documented DS4 reference snapshot, *not* a universal pinout for every ESP32-S3 board. Verify them against your own wiring before powering hardware. The XInput build shares the controller hardware, but an updated physical wiring audit is still recommended.

## Inputs

| Portal | DS4-style firmware | XInput firmware |
|---|---|---|
| Cross (×) | Cross | A |
| Circle (○) | Circle | B |
| Square (□) | Square | X |
| Triangle (△) | Triangle | Y |
| D-pad | D-pad/hat | D-pad buttons |
| L1 / R1 | L1 / R1 | LB / RB |
| L2 / R2 | Analog triggers | Analog triggers |
| L3 / R3 | Stick clicks | LS / RS |
| Start | Options | Start |
| Select | Touchpad click | Back |
| PS | PS | Guide / Home |
| Mute | Share in the DS4 mapping | Local LED function in the tested XInput build |

## Game testing (observations, not a compatibility guarantee)

| Game | DS4-style mode | XInput mode |
|---|---|---|
| Battlefield 6 | PlayStation layout and rumble observed | Xbox layout, native input and rumble observed |
| Zenless Zone Zero | PlayStation layout and lightbar observed; rumble not observed in that test | Xbox layout and combat/parry rumble observed |

Windows `joy.cpl` recognized the XInput build as **Controller (XBOX 360 For Windows)**. The native PS/Guide key also opened Xbox Game Bar on the tested PC.

## Project status and known limitations

- **Prototype hardware:** wires and flex breakouts still need final mechanical integration.
- **Haptics need further tuning.** Strong rumble could produce a startup click, and warmth was observed on the right actuator in some tests. Avoid unattended or extended high-power rumble until the drive waveform, wiring, current and thermal behavior are verified.
- Do **not** assume a fully replicated DS4: no physical touch surface, gyro, or original audio interfaces have been implemented.
- This is intended primarily for **wired Windows USB** use. Console compatibility, Bluetooth and other platforms have not been established.
- No combined DS4/XInput boot selector yet.
- Screenshot/recording button ideas are future work, not shipping features.
- The firmware folders in **this documentation starter** are placeholders until the exact, last-tested source snapshots are copied in. See [Publishing checklist](docs/PUBLISHING.md).

## Getting started

See [Build and flash](docs/BUILD_AND_FLASH.md). **Do not attempt to flash placeholders from this documentation-only starter.** Add the actual final `.ino`, `.cpp` and `.h` files from the working builds first.

## Where this came from

The XInput protocol research drew inspiration from [GP2040-CE](https://github.com/OpenStickCommunity/GP2040-CE), and the USB implementation was adapted for the ESP32-S3 Arduino/TinyUSB environment. This project is not GP2040-CE running on the ESP32-S3.

For external projects, licenses and acknowledgements, see [Credits](docs/CREDITS.md).

## Media

Photos, controller internals, and a short demo are planned. See [Showcase planning](docs/SHOWCASE.md).

## Licensing and trademarks

**License selection pending:** before distributing the code publicly as open source, verify the provenance of all third-party snippets and choose a compatible license. Do not assume that a project's license automatically applies just because it was used as a research reference. See [Publishing checklist](docs/PUBLISHING.md).

Sony, PlayStation, Microsoft, Xbox, and other product names are trademarks of their respective owners. Device VID/PID values used for compatibility research do not indicate an official partnership.
