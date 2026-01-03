# Enhanced Boot Restorer for TX-Ultimate-Easy

This Home Assistant Blueprint is a specialized enhancement for users of the [TX-Ultimate-Easy](https://github.com/edwardtfn/TX-Ultimate-Easy) project.

## 🚀 The Power of This Enhancement

While **TX-Ultimate-Easy** handles the hardware interaction of the Sonoff TX Ultimate (T5), this blueprint provides a **Software-side Management Layer** to bypass the need for re-flashing ESPHome whenever you want to change boot behaviors.

### Key Advantages:
- **Dynamic Configuration**: Change boot states (On/Off) instantly from your Home Assistant Dashboard using simple Dropdown Helpers.
- **Auto-Sync on Reconnect**: Ensures your relays return to the desired state whenever the device re-establishes a connection with Home Assistant.
- **Stealth Mode**: Automatically switches off the T5 LED ring indicator once the restoration sequence is finished.
- **Versatility**: Single blueprint that supports 1-gang, 2-gang, 3-gang, or 4-gang TX Ultimate models.

## 🛠 Setup Instructions

### 1. Create Helpers
For each relay channel, you must create an **Input Select (Dropdown)** helper:
- **Options**: `on`, `off`
- **Recommended naming**: `Living Room T5 Relay 1 Mode`

### 2. Import Blueprint
[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/MarcusTseng/tx-ultimate-relay-boot-mode/blob/main/blueprints/automation/tx_boot_mode/tx_relay_boot_mode.yaml)

### 3. Configure
In the Blueprint configuration UI:
1. Select the **Connectivity Sensor** (e.g., `sensor.*_device_name`).
2. Map your **Switch Entities** to their respective **Mode Helpers**.
3. (Optional) Select the **T5 Light Entity** to automate the status indicator shutdown.

## 🤝 Transparency & Credits
- **Core Hardware Logic**: Based on the excellent work by [edwardtfn/TX-Ultimate-Easy](https://github.com/edwardtfn/TX-Ultimate-Easy).
- **Development**: This blueprint's YAML logic and documentation were co-authored and optimized using **AI (Gemini)** to ensure clean code, flexible 1-4 gang support, and honest disclosure of tool usage.

## License
MIT