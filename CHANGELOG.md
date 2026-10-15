# Changelog

## DS4 v1.0 RC1 — reference checkpoint

- Functional DS4-style USB input mapping
- Feature report research (`0x02`, `0x12`, `0xA3`)
- Native gamepad input and Battlefield rumble tested
- Calibration, lightbar and hardware button handling

## XInput v0.4 — tested development checkpoint

- ESP32-S3 custom TinyUSB vendor-class driver
- Windows enumerates the device as `XBOX 360 For Windows`
- Full button/axis/trigger mapping ported from Portal input handling
- XInput rumble works in observed Battlefield and Zenless Zone Zero tests
- **Not yet declared final/stable:** haptic intensity, actuator warming and sustained-effect timeouts still need validation

## Planned

- Finish physical wiring and enclosure integration
- Measure actuator current/temperature, refine rumble waveform and timeout
- Selectable DS4/XInput mode at boot (experimental)
- Optional screenshot/recording action for the Mute button
