# Enhanced Boot Restorer for TX-Ultimate-Easy

(Version: 1.1.7)

This Home Assistant Blueprint is a specialized management layer designed to enhance the [TX-Ultimate-Easy](https://github.com/edwardtfn/TX-Ultimate-Easy) project for Sonoff TX Ultimate (T5) switches.

## 🚀 The Power of This Enhancement

While **TX-Ultimate-Easy** handles the hardware interaction, this blueprint adds a **Software-side Management Layer** to provide:
- **Dynamic UI Control**: Change boot behavior (On/Off) instantly via your Dashboard.
- **Auto-Sync on Reconnect**: Handles state restoration when the device recovers from `unavailable`.
- **Stealth Mode**: Automatically switches off the LED ring after the sequence.
- **Universal Support**: One blueprint for **1, 2, 3, or 4-gang** models.

## 📦 Installation & Setup

### 1. Import Blueprint
[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/MarcusTseng/tx-ultimate-relay-boot-mode/main/blueprints/automation/tx_boot_mode/tx_relay_boot_mode.yaml)

### 2. Configure Helpers & Automation
For each relay channel, you need an **Input Select (Dropdown)** helper with options `on` and `off`. You have two ways to create these:
- **Option A (Fastest)**: Directly click the **"+"** icon at the bottom of the helper dropdown menu while configuring this blueprint.
- **Option B (Manual)**: Go to **Settings > Devices & Services > Helpers** and create a Dropdown.

## ⚙️ Configuration Guide
1. **Connectivity Sensor**: Select the 'Device Name' sensor from your T5.
2. **Relays & Helpers**: Map Switch/Light entities to their Boot Mode Helpers. Leave unused channels empty.
3. **Status Light**: Map the T5 Light entity to automate the LED ring shutdown.

## 🤝 Transparency & Credits
- **Core Hardware Logic**: Based on [edwardtfn/TX-Ultimate-Easy](https://github.com/edwardtfn/TX-Ultimate-Easy).
- **AI-Assisted Development**: Developed and optimized with **AI (Gemini)** for clean code and flexible configuration.

## License
MIT