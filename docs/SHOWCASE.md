# Reddit / YouTube showcase plan

## What to demonstrate in a 45–75-second clip

1. **Hook:** original Portal controls in the modified hardware, with a caption: "Original PS Portal controls → native Xbox XInput on an ESP32-S3"
2. **Internals:** close-up of ESP32-S3, MCP23017, DRV8833 and USB-C breakout
3. **USB plug-in:** Windows `joy.cpl` shows `Controller (XBOX 360 For Windows)`
4. **Guide button:** Portal PS button opens Xbox Game Bar
5. **Gameplay:** show ABXY glyphs in Battlefield or ZZZ; demonstrate an in-game rumble event, ideally with a reaction/close-up
6. **Engineering angle:** short on-screen diagram of the custom TinyUSB vendor-class driver
7. **End:** GitHub link and honest notes about remaining thermal/haptics tuning

## Potential Reddit title

"I turned PlayStation Portal controller hardware into a native Xbox 360/XInput USB controller using an ESP32-S3 (with rumble!)"

## Potential YouTube title

"I Made the PlayStation Portal Work as a Native Xbox Controller — ESP32-S3 + XInput"

## Story to tell

- Started by decoding control flex cables and analog sensors
- Built a DS4-style HID firmware, encountered PC game mapping quirks
- Studied GP2040-CE's XInput descriptors and custom TinyUSB drivers
- Implemented a native Xbox-style USB interface on ESP32-S3 in Arduino
- Achieved real XInput behavior, including Xbox Game Bar and in-game rumble
- Left outstanding problems documented: thermal tuning, final packaging, boot-mode switching

## Shooting tips

Use original hardware close-ups; record a clean test bench before reassembling. Avoid sharing account names, serial numbers, other people's faces, or personal notifications. Capture footage with game audio rights in mind.
