# Enhanced Boot Restorer for TX-Ultimate-Easy

(Version: 1.2.2)

This Home Assistant Blueprint is a comprehensive management layer designed to enhance the [TX-Ultimate-Easy](https://github.com/edwardtfn/TX-Ultimate-Easy) project for Sonoff TX Ultimate (T5) switches.

## 🚀 The Power of This Enhancement

While **TX-Ultimate-Easy** handles the essential hardware interaction, this blueprint adds a software-side management layer to provide:

- **Dynamic UI Control**: Change boot behavior (On/Off) instantly via your Dashboard without flashing firmware.
- **Auto-Sync on Reconnect**: Handles state restoration automatically when the device recovers from an `unavailable` state.
- **Linked Device Sync**: Optimized for "Detached Mode." Ensures separate smart devices (e.g., Matter bulbs) controlled by the T5 button are synced correctly when the T5 boots up.
- **Customizable Timing (New)**: 
    - **Initial Delay**: Stability wait before triggering relays.
    - **Sync Delay**: Prevents "Timeout" errors for Matter/Zigbee devices by allowing time for network re-entry.
- **Stealth Mode**: Automatically turns off the LED ring indicator after the boot sequence completes.
- **Universal Support**: A single blueprint supporting **1, 2, 3, or 4-gang** models with clear UI grouping.

## 📦 Installation & Setup

### 1. Import Blueprint
[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/MarcusTseng/tx-ultimate-relay-boot-mode/main/blueprints/automation/tx_boot_mode/tx_relay_boot_mode.yaml)

### 2. Configure Helpers
For each relay channel, create an **Input Select (Dropdown)** helper with options `on` and `off`. You can do this directly within the blueprint configuration screen by clicking the **"+"** icon.

## ⚙️ Configuration Guide

1. **Connectivity Sensor**: Select the 'Device Name' sensor from your T5.
2. **Timing Settings**:
    - **Initial Delay**: Stability wait (default 5s).
    - **Sync Delay**: Set to **8-15s** for Matter devices to prevent timeouts.
3. **Channel Settings (1-4)**:
    - **Relay Switch**: The internal T5 relay.
    - **Linked Device**: The smart bulb/device controlled by this button.
    - **Keep Linked ON**: If disabled, the device will turn ON then OFF during sync (state reset).
4. **Status Light**: The T5 LED ring entity for automated cleanup.

## 🤝 Credits
- **Core Hardware Logic**: [edwardtfn/TX-Ultimate-Easy](https://github.com/edwardtfn/TX-Ultimate-Easy).
- **AI-Assisted Development**: Developed and optimized with **AI (Gemini)**.

## License
MIT