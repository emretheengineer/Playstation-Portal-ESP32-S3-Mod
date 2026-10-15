# Wiring reference — ESP32-S3 N16R8

These pin values are transcribed from the uploaded DS4 reference firmware. **They must be confirmed against the actual assembled unit before building from this guide.** ESP32-S3 board variants differ, and some pins have boot-time or USB-related constraints.

## Native USB-C breakout

| Signal | ESP32-S3 |
|---|---|
| USB D− | GPIO 19 |
| USB D+ | GPIO 20 |
| USB VBUS | 5V input / board-appropriate VBUS path |
| GND | GND |

Use a breakout correctly configured for **USB-C device / UFP** operation (CC pull-down resistors when needed); verify VBUS routing and avoid feeding the board from conflicting supplies. Do not connect USB VBUS to a 3.3V GPIO.

## MCP23017

I²C SDA: GPIO 47; SCL: GPIO 48; address: `0x20`.

| MCP index | Control |
|---|---|
| 0 / GPA0 | PS |
| 1 / GPA1 | Select |
| 2 / GPA2 | Mute LED common |
| 3 / GPA3 | Mute LED active-low |
| 4 / GPA4 | Start |
| 5 / GPA5 | Mute |
| 6 / GPA6 | Triangle |
| 7 / GPA7 | Square |
| 8 / GPB0 | RGB / former pairing button |
| 9 / GPB1 | L1 |
| 10 / GPB2 | R1 |

## Direct inputs

| Function | GPIO |
|---|---:|
| D-pad right | 4 |
| D-pad up | 5 |
| D-pad left | 6 |
| D-pad down | 7 |
| Circle | 41 |
| Cross | 42 |
| L2 analog | 15 |
| R2 analog | 14 |
| L3 click | 46 |
| R3 click | 21 |
| Left stick X | 10 |
| Left stick Y | 9 |
| Right stick X | 2 |
| Right stick Y | 1 |

## RGB lightbar — active low

| Channel | Left GPIO | Right GPIO |
|---|---:|---:|
| Red | 17 | 13 |
| Green | 18 | 12 |
| Blue | 8 | 11 |

## DRV8833 haptics

| Input | GPIO |
|---|---:|
| Left IN1 | 38 |
| Left IN2 | 16 |
| Right IN1 | 40 |
| Right IN2 | 39 |

The actuators are non-standard relative to ordinary Xbox eccentric-rumble motors. Thermal/current safety is **not fully characterized**; do not leave the actuator driven indefinitely. Stop if the right-side actuator stays warm when it should be idle.

## Needed before calling the hardware documentation final

- Confirm the exact ESP32-S3 carrier board and electrical supply rails
- Photograph/label original flex-cable connections and breakouts
- Verify common grounds and USB-C CC resistors
- Add a wiring diagram and current measurements under continuous rumble
