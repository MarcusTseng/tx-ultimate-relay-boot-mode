# TX Ultimate relay boot mode (Home Assistant blueprint)

This repository contains a Home Assistant automation blueprint to control
the boot behavior of relays on Sonoff TX Ultimate switches.

It lets you define, per relay, whether it should:
- **Default** follow the default ESPHome / TX-Ultimate-Easy restore behavior,
- **Force ON** after the device boots, or
- **Force OFF** after the device boots.

The blueprint supports 1/2/3/4‑gang TX Ultimate devices.

---

## Naming convention

To keep things simple and consistent across devices, this blueprint assumes
the following entity naming scheme for each TX Ultimate switch:

- Relays:
  - `switch.xxx_relay_1`
  - `switch.xxx_relay_2`
  - `switch.xxx_relay_3`
  - `switch.xxx_relay_4`

- Helpers (input_select) for boot mode:
  - `input_select.xxx_relay_1_boot_mode`
  - `input_select.xxx_relay_2_boot_mode`
  - `input_select.xxx_relay_3_boot_mode`
  - `input_select.xxx_relay_4_boot_mode`

Where `xxx` is the common name prefix of the device, for example:

```text
xxx = t5_4c_120_01

switch.t5_4c_120_01_relay_1
input_select.t5_4c_120_01_relay_1_boot_mode
...
