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
Each input_select.xxx_relay_n_boot_mode should have three options:

Default

Force ON

Force OFF

Default means “do nothing” and let TX-Ultimate-Easy / ESPHome handle the
restore behavior.

Installation
Copy the blueprint file

Place the blueprint file in your Home Assistant configuration directory:

text
config/blueprints/automation/tx_boot_mode/tx_relay_boot_mode.yaml
If you clone this repository directly into your HA config, the path will look like:

text
config/tx-ultimate-relay-boot-mode/blueprints/automation/tx_boot_mode/tx_relay_boot_mode.yaml
In that case, move the tx_boot_mode folder (or the YAML file) into
config/blueprints/automation/.

Reload blueprints

In Home Assistant:

Go to Settings → Automations & Scenes → Blueprints

Click ⋮ → Reload Blueprints

You should now see a blueprint named:

TX Ultimate relay boot mode (1–4 gang, fixed naming)

Create the helpers

For each relay you want to control, create a matching input_select
helper in Home Assistant (Settings → Devices & Services → Helpers):

input_select.xxx_relay_1_boot_mode

input_select.xxx_relay_2_boot_mode

input_select.xxx_relay_3_boot_mode

input_select.xxx_relay_4_boot_mode

Each helper should have these options:

text
Default
Force ON
Force OFF
Using the blueprint
Go to Settings → Automations & Scenes → Blueprints.

Click the blueprint TX Ultimate relay boot mode (1–4 gang, fixed naming).

Click Create automation.

Fill in:

Name prefix: for example t5_4c_120_01

Gang count: choose 1, 2, 3, or 4 depending on your device.

Save the automation.

From now on, whenever the TX Ultimate device reboots and its relays restore
state in Home Assistant, the automation will:

wait a short delay, then

for each relay:

if the corresponding helper is Force ON, turn the relay on (only if not already on);

if the helper is Force OFF, turn the relay off (only if not already off);

if the helper is Default, do nothing.

This keeps the original TX-Ultimate-Easy boot logic intact while giving you
an extra layer of control from Home Assistant.
