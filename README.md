# Enhanced Boot Restorer for TX-Ultimate-Easy

(Version: 1.1.5)

This Home Assistant Blueprint is a specialized management layer designed to enhance the [TX-Ultimate-Easy](https://github.com/edwardtfn/TX-Ultimate-Easy) project for Sonoff TX Ultimate (T5) switches.

## 🚀 The Power of This Enhancement

While **TX-Ultimate-Easy** handles the core hardware logic of the Sonoff T5, this blueprint provides a **Dynamic Management Layer** within Home Assistant. This allows you to bypass the need for re-flashing ESPHome whenever you want to change power-on/reconnection behaviors.

### Key Features:
- **Dynamic Boot Logic**: Change relay boot states (on/off) instantly from your HA Dashboard using simple Dropdown Helpers. No YAML editing or flashing required.
- **Reconnection Sync**: Specifically handles state restoration when the device recovers from an `unavailable` status (e.g., after a Wi-Fi drop or HA restart).
- **Stealth Mode (Status Cleanup)**: Automatically switches off the T5 LED ring indicator once the restoration sequence is finished, maintaining a clean look.
- **Network Optimization**: Uses "check-before-action" logic to only send commands if the current state differs from the target, reducing Zigbee/Wi-Fi traffic.
- **Universal Support**: One blueprint that flexibly supports **1-gang, 2-gang, 3-gang, or 4-gang** TX Ultimate models.

## 🛠 Prerequisites

Before using this blueprint, you must create **Input Select (Dropdown)** helpers for each relay channel:
1. Go to **Settings > Devices & Services > Helpers**.
2. Create a **Dropdown** with the following options:
   - `on`
   - `off`
3. We recommend naming them consistently, e.g., `Living Room T5 Relay 1 Mode`.

## 📦 Installation

Click the button below to import this blueprint directly into your Home Assistant instance:

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/MarcusTseng/tx-ultimate-relay-boot-mode/main/blueprints/automation/tx_boot_mode/tx_relay_boot_mode.yaml)

*Manual Import URL:* `https://raw.githubusercontent.com/MarcusTseng/tx-ultimate-relay-boot-mode/main/blueprints/automation/tx_boot_mode/tx_relay_boot_mode.yaml`

## ⚙️ Configuration Guide

1. **Connectivity Sensor**: Select the 'Device Name' sensor provided by TX-Ultimate-Easy.
2. **Relays & Helpers**: 
   - **Relay 1**: Required for all models.
   - **Relay 2-4**: Optional. Leave these and their corresponding helpers empty if your device has fewer channels (e.g., leave 3 and 4 empty for a 2-gang switch).
3. **Status Light**: Map this to the T5 Light entity to enable the automatic LED ring shutdown feature.

## 🤝 Transparency & Credits
- **Core Hardware Logic**: This project is built to complement [edwardtfn/TX-Ultimate-Easy](https://github.com/edwardtfn/TX-Ultimate-Easy).
- **AI-Assisted Development**: This blueprint's logic, structure, and documentation were co-authored and optimized with the assistance of **AI (Gemini)** to ensure clean code, flexible multi-channel support, and reliable performance.

## License
MIT