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
```
Each input_select.xxx_relay_n_boot_mode should have three options:

Default
Force ON
Force OFF

Default means “do nothing” and let TX-Ultimate-Easy / ESPHome handle the
restore behavior.


Installation
1. Copy the blueprint file

Place the blueprint file in your Home Assistant configuration directory:

```text
config/blueprints/automation/tx_boot_mode/tx_relay_boot_mode.yaml
```
If you clone this repository directly into your HA config, the path will look like:

```text
config/tx-ultimate-relay-boot-mode/blueprints/automation/tx_boot_mode/tx_relay_boot_mode.yaml
```
In that case, move the tx_boot_mode folder (or the YAML file) into
config/blueprints/automation/.

2. Reload blueprints

In Home Assistant:

Go to Settings → Automations & Scenes → Blueprints
Click ⋮ → Reload Blueprints

You should now see a blueprint named:
  TX Ultimate relay boot mode (1–4 gang, fixed naming)

3. Create the helpers

For each relay you want to control, create a matching input_select
helper in Home Assistant (Settings → Devices & Services → Helpers):

- input_select.xxx_relay_1_boot_mode
- input_select.xxx_relay_2_boot_mode
- input_select.xxx_relay_3_boot_mode
- input_select.xxx_relay_4_boot_mode

Each helper should have these options:
```text
Default
Force ON
Force OFF
```
Using the blueprint
1. Go to Settings → Automations & Scenes → Blueprints.
2. Click the blueprint TX Ultimate relay boot mode (1–4 gang, fixed naming).
3. Click Create automation.
4. Fill in:
    - Name prefix: for example t5_4c_120_01
    - Gang count: choose 1, 2, 3, or 4 depending on your device.
5. Save the automation.

From now on, whenever the TX Ultimate device reboots and its relays restore
state in Home Assistant, the automation will:
- wait a short delay, then
- for each relay:
    -if the corresponding helper is Force ON, turn the relay on (only if not already on);
    -if the helper is Force OFF, turn the relay off (only if not already off);
    -if the helper is Default, do nothing.

This keeps the original TX-Ultimate-Easy boot logic intact while giving you
an extra layer of control from Home Assistant.
```text

```yaml
blueprint:
  name: TX Ultimate relay boot mode (1–4 gang, fixed naming)
  description: >
    Set per-relay boot behavior (Default / Force ON / Force OFF) for a
    Sonoff TX Ultimate using fixed naming:
      - Relays: switch.xxx_relay_1..4
      - Helpers: input_select.xxx_relay_1_boot_mode..4_boot_mode
    Supports 1/2/3/4‑gang devices.
  domain: automation
  author: you

  input:
    name_prefix:
      name: Name prefix (xxx)
      description: >
        Common name used for this switch. Relays must be:
          switch.xxx_relay_1..4
        and helpers must be:
          input_select.xxx_relay_1_boot_mode..4_boot_mode
      selector:
        text:

    gang_count:
      name: Gang count
      description: How many relays (gangs) this switch has
      default: 4
      selector:
        select:
          options:
            - 1
            - 2
            - 3
            - 4

mode: single

trigger:
  - platform: state
    entity_id:
      - "{{ 'switch.' ~ (name_prefix | string) ~ '_relay_1' }}"
      - "{{ 'switch.' ~ (name_prefix | string) ~ '_relay_2' }}"
      - "{{ 'switch.' ~ (name_prefix | string) ~ '_relay_3' }}"
      - "{{ 'switch.' ~ (name_prefix | string) ~ '_relay_4' }}"

variables:
  name_prefix: !input name_prefix
  gang_count: !input gang_count

  relay_1: "{{ 'switch.' ~ name_prefix ~ '_relay_1' }}"
  relay_2: "{{ 'switch.' ~ name_prefix ~ '_relay_2' }}"
  relay_3: "{{ 'switch.' ~ name_prefix ~ '_relay_3' }}"
  relay_4: "{{ 'switch.' ~ name_prefix ~ '_relay_4' }}"

  helper_1: "{{ 'input_select.' ~ name_prefix ~ '_relay_1_boot_mode' }}"
  helper_2: "{{ 'input_select.' ~ name_prefix ~ '_relay_2_boot_mode' }}"
  helper_3: "{{ 'input_select.' ~ name_prefix ~ '_relay_3_boot_mode' }}"
  helper_4: "{{ 'input_select.' ~ name_prefix ~ '_relay_4_boot_mode' }}"

action:
  - delay: "00:00:03"

  # Relay 1
  - choose:
      - conditions:
          - condition: template
            value_template: "{{ states(helper_1) == 'Force ON' }}"
        sequence:
          - condition: template
            value_template: "{{ states(relay_1) != 'on' }}"
          - service: switch.turn_on
            target:
              entity_id: "{{ relay_1 }}"
      - conditions:
          - condition: template
            value_template: "{{ states(helper_1) == 'Force OFF' }}"
        sequence:
          - condition: template
            value_template: "{{ states(relay_1) != 'off' }}"
          - service: switch.turn_off
            target:
              entity_id: "{{ relay_1 }}"
    default: []

  # Relay 2
  - choose:
      - conditions:
          - condition: template
            value_template: "{{ gang_count|int >= 2 and states(helper_2) == 'Force ON' }}"
        sequence:
          - condition: template
            value_template: "{{ states(relay_2) != 'on' }}"
          - service: switch.turn_on
            target:
              entity_id: "{{ relay_2 }}"
      - conditions:
          - condition: template
            value_template: "{{ gang_count|int >= 2 and states(helper_2) == 'Force OFF' }}"
        sequence:
          - condition: template
            value_template: "{{ states(relay_2) != 'off' }}"
          - service: switch.turn_off
            target:
              entity_id: "{{ relay_2 }}"
    default: []

  # Relay 3
  - choose:
      - conditions:
          - condition: template
            value_template: "{{ gang_count|int >= 3 and states(helper_3) == 'Force ON' }}"
        sequence:
          - condition: template
            value_template: "{{ states(relay_3) != 'on' }}"
          - service: switch.turn_on
            target:
              entity_id: "{{ relay_3 }}"
      - conditions:
          - condition: template
            value_template: "{{ gang_count|int >= 3 and states(helper_3) == 'Force OFF' }}"
        sequence:
          - condition: template
            value_template: "{{ states(relay_3) != 'off' }}"
          - service: switch.turn_off
            target:
              entity_id: "{{ relay_3 }}"
    default: []

  # Relay 4
  - choose:
      - conditions:
          - condition: template
            value_template: "{{ gang_count|int >= 4 and states(helper_4) == 'Force ON' }}"
        sequence:
          - condition: template
            value_template: "{{ states(relay_4) != 'on' }}"
          - service: switch.turn_on
            target:
              entity_id: "{{ relay_4 }}"
      - conditions:
          - condition: template
            value_template: "{{ gang_count|int >= 4 and states(helper_4) == 'Force OFF' }}"
        sequence:
          - condition: template
            value_template: "{{ states(relay_4) != 'off' }}"
          - service: switch.turn_off
            target:
              entity_id: "{{ relay_4 }}"
    default: []
```
