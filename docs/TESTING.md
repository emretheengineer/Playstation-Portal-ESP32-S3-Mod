# Test log and reproducibility

The statuses below summarize hands-on observations from the development conversation; they are not formal certification or a guarantee across all PCs/games.

| Check | Observed result | Further work |
|---|---|---|
| USB XInput enumeration on Windows | `Controller (XBOX 360 For Windows)` | Test more OS versions |
| Face buttons, shoulders, D-pad | Worked in Windows `joy.cpl` | Final all-input video |
| Xbox Guide / Portal PS button | Opened Xbox Game Bar | Verify OS setting dependencies |
| Battlefield 6 in XInput mode | Xbox layout, input and rumble observed | Longer stability/thermal tests |
| Zenless Zone Zero in XInput mode | Xbox layout and vibration during combat/parry observed | Long-term testing |
| Battlefield 6 in DS4 mode | PlayStation prompts and rumble observed | Test multiple builds |
| Zenless Zone Zero in DS4 mode | PlayStation prompts/lightbar; no rumble in observed tests | May be game-specific |
| Haptic actuator heating | Right actuator sometimes became warm | Investigate before stable release |
| Continuous firing rumble | Watchdog-related interruptions investigated | Re-test with exact final firmware |

## Pre-release checklist

- [ ] Ensure no actuator warms in the idle state
- [ ] Verify stop signal and USB disconnection shut off output
- [ ] Verify button/stick mapping in `joy.cpl`
- [ ] Verify USB reconnect behavior
- [ ] Check trigger full-range calibration
- [ ] 10-minute gameplay smoke test with temperature checks
- [ ] Save core and library versions used
- [ ] Keep a backup of the source files and known-good binary
