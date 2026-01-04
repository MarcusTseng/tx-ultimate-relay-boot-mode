# Enhanced Boot Restorer for TX-Ultimate-Easy

(Version: 1.3.6)

This Home Assistant Blueprint is a specialized software management layer designed to enhance the [TX-Ultimate-Easy](https://github.com/edwardtfn/TX-Ultimate-Easy) project for Sonoff TX Ultimate (T5) switches.

## 🚀 Installation & Setup

### 1. Import Blueprint
[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/MarcusTseng/tx-ultimate-relay-boot-mode/main/blueprints/automation/tx_boot_mode/tx_relay_boot_mode.yaml)

### 2. Configure Automation
Map your internal T5 relays to their desired boot states and optional linked smart devices directly in the UI.

## 💎 The Power of This Enhancement

- **Fault-Tolerant Execution (v1.3.6)**: Linked device synchronization is now non-blocking. If a command fails (e.g., Matter timeout), the automation will continue processing other tasks without erroring out.
- **Parallel Processing**: All relay channels operate independently in parallel. A delay on one channel will not block the others.
- **Smart Availability Wait**: The system waits for each linked device to report as "available" before syncing, eliminating blind timeout errors.
- **Dynamic UI Control**: Set relay boot states (On/Off) directly within the configuration screen. No external helpers required.
- **Auto-Sync on Reconnect**: Restores states automatically when the device recovers from an `unavailable` state.
- **Stealth Mode**: Automatically turns off the LED ring indicator after sequences complete.
- **Minimum HA Requirement**: **2025.12.0**.

## 🤝 Credits
- **Core Hardware Logic**: [edwardtfn/TX-Ultimate-Easy](https://github.com/edwardtfn/TX-Ultimate-Easy).
- **AI-Assisted Development**: Developed and optimized with **AI (Gemini)**.

## License
MIT