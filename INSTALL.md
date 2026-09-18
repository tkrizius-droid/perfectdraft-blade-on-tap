# Installation Guide

This project has two parts:

1. **Frontend assets** — installed by HACS as a Dashboard repository.
2. **Home Assistant helpers/templates/automations** — installed from the package YAML.

## Before you start

Required:
- Home Assistant
- HACS
- Button Card (`custom:button-card`)

For PerfectDraft Pro:
- PerfectDraft Pro integration by Falkvinge: `Falkvinge/hassio-integration-perfectdraft-pro`

The Blade card does not require a Blade integration.

---

## A. Install the frontend with HACS

1. Open **HACS**.
2. Go to **Dashboard**.
3. Open **⋮ → Custom repositories**.
4. Add:
   `https://github.com/tkrizius-droid/perfectdraft-blade-on-tap`
5. Category: **Dashboard**.
6. Install **PerfectDraft + Blade On Tap**.
7. Reload Home Assistant when HACS prompts you.

HACS installs the repository frontend files under:

`/config/www/community/perfectdraft-blade-on-tap/`

The dashboard references them through:

`/hacsfiles/perfectdraft-blade-on-tap/`

### Quick asset test

Open this path in your Home Assistant browser:

`/hacsfiles/perfectdraft-blade-on-tap/perfectdraft/neutral-keg-t3.png`

If the neutral keg image loads, the HACS asset install is working.

---

## B. Install Button Card

Install **Button Card** in HACS if it is not already installed.

The dashboard uses:

`custom:button-card`

Reload/restart Home Assistant if HACS asks you to.

---

## C. Install the Home Assistant package

Copy:

`packages/perfectdraft_on_tap.yaml`

to:

`/config/packages/perfectdraft_on_tap.yaml`

If packages are not already enabled, add this under your existing `homeassistant:` section:

```yaml
homeassistant:
  packages: !include_dir_named packages
```

Do not create a second `homeassistant:` key if one already exists.

Then:
1. Check Home Assistant configuration.
2. Restart Home Assistant.

The package creates:
- Blade current-keg selector
- Blade insertion date/time helper
- Blade 14-pint counter
- Blade freshness sensor
- PerfectDraft current-keg selector
- PerfectDraft ABV sensor
- PerfectDraft pints-remaining sensor
- PerfectDraft pours-this-keg sensor
- three Blade automations

### Important for existing installations

If you already have helpers/entities with the same IDs, **do not install the package again**. Duplicate YAML definitions can cause configuration errors. Existing users should keep their current entities and use the entity mapping in `reference/ENTITY_MAPPING.md`.

---

## D. Configure PerfectDraft Pro

Install and configure the PerfectDraft Pro integration.

The public dashboard expects these integration entities:

- `sensor.perfectdraft_pro_temperature`
- `sensor.perfectdraft_pro_keg_remaining`
- `sensor.perfectdraft_pro_keg_freshness`
- `sensor.perfectdraft_pro_pours`

Home Assistant entity IDs can differ if an entity was renamed. If yours differ, replace the matching references in the dashboard YAML.

---

## E. Import the dashboard

For a HACS installation, use:

`dashboard/on_tap_hacs.yaml`

Create a new dashboard or view, open the **Raw configuration editor**, and paste the YAML.

For a manual asset installation under `/config/www/perfectdraft/`, use:

`dashboard/on_tap.yaml`

---

## F. Select your keg

Use:
- `input_select.blade_current_keg`
- `input_select.perfectdraft_current_keg`

When the Blade keg changes, the included automations:
- stamp the insertion date/time
- reset the Blade counter to 14 pints

The daily countdown reduces the Blade counter by one at midnight; use the + / − controls on the card for manual correction.

---

## Optional theme

Copy:

`themes/perfectdraft.yaml`

to:

`/config/themes/perfectdraft.yaml`

The theme can use card-mod if installed.

---

## Uninstall

HACS frontend:
- HACS → PerfectDraft + Blade On Tap → Remove.

Package:
- remove `/config/packages/perfectdraft_on_tap.yaml`
- check configuration
- restart Home Assistant

Removing the package also removes the YAML-defined helpers/templates/automations on restart, so note any values you want to preserve first.
