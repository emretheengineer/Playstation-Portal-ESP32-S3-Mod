# Firmware architecture

## Shared physical layers

The input layer reads several classes of control:

- GPIO buttons and the D-pad
- MCP23017 expander buttons
- Analog joysticks and trigger sensors
- Calibration values saved in ESP32 NVS/Preferences

The output layer controls RGB lightbars, a Mute status LED, and the DRV8833-driven Portal haptics.

## DS4-style firmware

- Built on Arduino's USB HID support
- Uses a DS4-style input report and selected feature reports (`0x02`, `0x12`, `0xA3`)
- Games may show PlayStation button glyphs
- DS4 USB output messages carry rumble/lightbar commands
- Does not implement all original hardware, such as audio or motion sensing

## Native XInput firmware

The XInput development followed GP2040-CE protocol research but uses an ESP32-S3-specific implementation:

1. Arduino-ESP32 and TinyUSB expose a custom class-driver hook, `usbd_app_driver_get_cb()`.
2. A vendor-class USB gamepad interface opens interrupt IN and OUT endpoints.
3. A **20-byte** wired Xbox 360-style input report carries buttons, analog triggers, and signed 16-bit stick values.
4. USB OUT packets carry rumble motor commands.
5. The driver forwards the intensity values to the DRV8833 haptic layer.

Observed on Windows: `Controller (XBOX 360 For Windows)` in `joy.cpl`; Xbox Guide button opens Game Bar.

**Why separate builds?** USB protocol identities and class drivers are selected before the host enumerates the device. No runtime selection between DS4 and XInput exists yet.

## Safety note

The XInput host may issue a motor level and expect the controller to maintain that level until another output packet arrives. Meanwhile, the original haptic engine used a short safety timeout. Rumble-latching vs safety shutdown and actuator heating remain under investigation. Do not publish untested watchdog alterations as a stable release.
