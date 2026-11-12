Clean upstream ZapFast updated to upstream v0.21.1 with modular local plugins and personal enhancements.

## What's Changed in v0.21.1

### Upstream v0.21.1 Features & Improvements
* **Calls & Media:** In-app audio/video calling, call tones, diagnostic logs, and audio pipeline improvements.
* **Chat Management:** Chat export, disappearing messages worker, and contact blocking.
* **Visuals & UX:** Lottie animations, attachment preview overhaul, motion controls, improved image editor, and backdrop effects.
* **Accessibility:** Enhanced screen-reader announcer and accessibility labels across UI elements.
* **Performance:** Prefetching workers, download management, and link preview settings.

### Better-ZapFast Personal Features & Plugins
* **Modular Plugin Host:** Rhai script-based plugin host supporting live-reloading plugins without rebuilding.
* **Built-in Plugins:**
  * **Quoter:** Direct message quote cards with full avatars, contextual quote action, and localized Turkish/Spanish support.
  * **Anti-Delete:** Retains deleted messages and preserves media attachments locally.
  * **Auto-Reply:** Flexible /command listeners and automated responses configurable in Settings.
  * **Notification Throttle:** Per-chat / per-account notification rate limiting (default 30s interval).
  * **Quick Stickers:** Fast sticker picker button right next to the emoji bar.
  * **Bugfix:** Chat header overflow layout bounds and static sticker previews during animation decoding.
  * **Quality of Life:** Ctrl + Mouse1 drag selection policy for messages.
* **Windows GUI:** Console-free window launch (Windows subsystem mode).

## Verification
* Cargo test suite: all targets and features passing (2,548 passed, 0 failed).
* Clippy: `-D warnings` clean across all targets and all features.
* Tested on Windows 11 x64.

## Notes & Limits
* This release targets Windows x64. Plugin scripts and user data remain stored in `%APPDATA%\paolino\zapfast\config\plugins`.
* Upstream ZapFast project: [crmne/zapfast](https://github.com/crmne/zapfast).
