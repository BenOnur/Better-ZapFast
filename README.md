<p align="center">
  <img src="docs/assets/images/logo.svg" alt="Better-ZapFast logo" width="80" height="80">
</p>

<h1 align="center">Better-ZapFast</h1>

<p align="center">
  <strong>Native, blazingly fast WhatsApp desktop client with an extensible Rhai plugin engine.</strong><br>
  A power-user fork of <a href="https://github.com/crmne/zapfast">ZapFast</a> designed for speed, privacy, and full client-side control.
</p>

<p align="center">
  <a href="https://github.com/BenOnur/Better-ZapFast/releases/latest"><img src="https://img.shields.io/github/v/release/BenOnur/Better-ZapFast?color=00a884&label=release&style=flat-square" alt="Latest Release"></a>
  <a href="Cargo.toml"><img src="https://img.shields.io/badge/Rust-2024%20Edition-dea584?style=flat-square&logo=rust&logoColor=white" alt="Built with Rust"></a>
  <img src="https://img.shields.io/badge/Platform-Windows%20x64-0078d4?style=flat-square&logo=windows&logoColor=white" alt="Windows x64">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-00a884?style=flat-square" alt="MIT License"></a>
  <a href="https://github.com/BenOnur/zapfast-plugins"><img src="https://img.shields.io/badge/Plugins-Catalog-blueviolet?style=flat-square" alt="Plugin Catalog"></a>
</p>

<p align="center">
  <a href="#key-enhancements">Key Enhancements</a> •
  <a href="#built-in-plugins">Plugins</a> •
  <a href="#installation">Installation</a> •
  <a href="#how-it-works">How It Works</a> •
  <a href="#acknowledgements">Acknowledgements</a>
</p>

---

<picture>
  <source media="(prefers-color-scheme: light)" srcset="docs/screenshot-light.png">
  <img src="docs/screenshot.png" alt="Better-ZapFast Interface Preview" width="100%">
</picture>

## Overview

**Better-ZapFast** extends the lightweight, native architecture of [ZapFast](https://github.com/crmne/zapfast) by embedding an in-app Rhai scripting runtime. It allows you to write, modify, and reload custom client behaviors, layout rules, and message handlers on the fly—without recompiling the binary.

Built with Rust, [egui](https://www.egui.rs), and [fastframe](https://fastframe.dev), Better-ZapFast runs with zero browser engine overhead, starting in under a second and using ~200 MB of idle memory (compared to ~1.1 GB in WhatsApp Web / Electron wrappers).

## Key Enhancements

* **Zero-Rebuild Plugin Architecture**: Modify or add plugins via plain `.rhai` scripts and `.json` manifests under `%APPDATA%\paolino\zapfast\config\plugins`. Hot-reload them anytime from *Settings > Plugins*.
* **Sandboxed & Safe Scripting**: The Rhai engine enforces strict operational boundaries (25,000 operation execution limit, 128 KiB state quotas, recursion limits, and suppression of log output).
* **Silent Windows Subsystem**: Configured as a native Windows GUI application—no lingering console windows or development terminal popups.
* **Deleted Media & Message Retention**: Preserves revoked content locally before WhatsApp deletes it from view.
* **Granular UI & Interaction Policies**: Full control over composer actions, message selection sweeps, and custom layout dimensions.

## Built-in Plugins

Better-ZapFast ships with support for several modular plugins, also available via the [zapfast-plugins](https://github.com/BenOnur/zapfast-plugins) catalog:

| Plugin | Hooks | Description |
|---|---|---|
| **Anti-Delete** | `on_before_delete`, `on_cache_media` | Retains deleted messages and proactively caches incoming media attachments (up to 64 MiB). |
| **Quoter** | `on_context_menu`, `on_card` | Creates Equicord/Discord-style quote cards with high-resolution avatars, dark/light themes, and exportable PNGs. |
| **Auto Responder** | `on_message` | Listens for configurable `/commands` in selected chats and sends automated replies with adjustable delay timers. |
| **Notification Throttle** | `on_notification` | Limits notification spam by enforcing a per-sender quiet window (e.g., 30s) across individual contacts. |
| **Quick Stickers** | `on_composer_tools` | Places a direct sticker picker shortcut immediately next to the emoji button for instant access. |
| **Bugfix** | `on_layout`, `on_media_policy` | Restores header title expansion on wide windows and enables immediate static sticker previews while animated WebP decodes. |
| **Quality of Life** | `on_input_policy` | Enforces `Ctrl + Left Click` for multi-message drag selection, preserving standard text selection without accidental sweeping. |

## Installation

### Windows (Pre-built Binaries)

1. Download the latest release archive (`zapfast-v<version>-x86_64-pc-windows-msvc.zip`) from [Releases](https://github.com/BenOnur/Better-ZapFast/releases/latest).
2. Extract the folder to your preferred application directory (e.g., `D:\Apps\ZapFast` or `C:\Program Files\ZapFast`).
3. Run `zapfast.exe`. The application operates in portable mode when `zapfast-portable.txt` is present beside the executable.

### Building from Source

Ensure you have a modern Rust toolchain installed:

```sh
# Clone repository
git clone https://github.com/BenOnur/Better-ZapFast.git
cd Better-ZapFast

# Run tests
cargo test --locked --all-targets

# Build optimized release binary
cargo build --locked --release
```

The resulting binary will be at `target/release/zapfast.exe`.

## Pairing Your Phone

1. Launch Better-ZapFast. A pairing QR code will be displayed.
2. On your mobile phone, navigate to **WhatsApp > Settings > Linked Devices > Link a Device**.
3. Scan the QR code, or select **Link with phone number** and enter the eight-character code.
4. Your recent chats will stream directly to your local encrypted database.

*Note: The link survives restarts, and your phone does not need to stay online once local history has synced.*

## Plugin Development

Custom plugins live in `%APPDATA%\paolino\zapfast\config\plugins/<plugin_id>/`:

```
<plugin_id>/
├── plugin.json    # Manifest defining API version, metadata, settings schema, and hooks
└── main.rhai      # Rhai script implementing corresponding event handlers
```

Refer to [docs/local-plugins.md](docs/local-plugins.md) for full API hook definitions, state management, and sample manifests.

## Acknowledgements

Better-ZapFast is a fork of [ZapFast](https://github.com/crmne/zapfast), originally created by **[Carmine Paolino](https://github.com/crmne)**.

* Upstream project: [crmne/zapfast](https://github.com/crmne/zapfast)
* Official project website: [zapfast.rocks](https://zapfast.rocks)
* WhatsApp protocol engine: [whatsapp-rust](https://github.com/oxidezap/whatsapp-rust)
* UI & framework: [egui](https://github.com/emilk/egui) & [fastframe](https://fastframe.dev)
* Typography & Assets: [Inter](https://rsms.me/inter/) font, Noto Color Emoji (OFL), and [Lucide](https://lucide.dev) icons.

*Disclaimer: Better-ZapFast is an independent, unofficial project and is not affiliated with, sponsored, or endorsed by WhatsApp LLC or Meta Platforms, Inc. Use at your own discretion.*

## License

Licensed under the [MIT License](LICENSE).
