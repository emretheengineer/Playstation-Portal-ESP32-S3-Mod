# Before publishing a firmware release

## Firmware snapshots

- [ ] Copy **your exact final tested** DS4 sources into `firmware/ds4/` (same sketch-directory filename rule as Arduino).
- [ ] Copy **your exact final tested** XInput sources into `firmware/xinput/`.
- [ ] Replace this starter's folder README placeholders with the actual files.
- [ ] Do not label XInput `v1.0 stable` until the haptic thermal behavior and watchdog strategy are confirmed.
- [ ] Compile both firmware variants independently; do not mix their `.cpp/.h` files into one sketch folder.
- [ ] Save the final Arduino-ESP32 core version, libraries, board-menu options and smoke-test evidence.
- [ ] Review any copied upstream protocol code and license headers.

## Licensing

Choose a license intentionally and place the full license text in `LICENSE` when you decide. For simple permissive sharing, consider MIT, but verify that all included third-party source is compatible. If no license is provided, public source is **not automatically open source** under an OSI license.

## Safety and privacy

- [ ] Confirm USB power routing and no shorts.
- [ ] Keep high-power haptics conservative until current/temperature are measured.
- [ ] Review firmware for unique MAC addresses, personal paths, passwords, tokens or serial identifiers before committing.
- [ ] Crop screenshots so Windows usernames, file paths, account profiles, and notifications aren't revealed.
- [ ] Avoid including commercially distributed game footage/audio in repository assets without considering rights.

## Publish through GitHub

1. Add and review the source files inside their respective sketch folders.
2. Check relative Markdown links and Mermaid rendering.
3. Add your own photos to `media/` and embed a real hero photo in `README.md`.
4. Tag a release only for a build that exactly matches tested source files.

Reference: https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository
