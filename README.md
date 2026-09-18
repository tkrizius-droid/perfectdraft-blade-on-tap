# PerfectDraft + Blade On Tap for Home Assistant

A Home Assistant dashboard for **PerfectDraft Pro** and **Blade** keg systems, with keg artwork, glass recommendations, country flags, freshness, ABV, temperature, remaining volume and Blade pint tracking.

> This repository is being prepared for HACS-friendly distribution. The dashboard itself is usable now; HACS can manage the dashboard assets once the `dist/` package is populated.

## What this project includes

- PerfectDraft Pro card with live temperature, freshness, keg remaining and beer details
- Blade card with manual keg selection, 14-pint counter and 30-day freshness tracking
- Beer artwork for PerfectDraft and Blade
- Recommended glass artwork and country flags
- Home Assistant package YAML for required helpers/templates/automations
- Optional PerfectDraft visual theme

## Requirements

- Home Assistant
- HACS
- **Button Card** (`custom:button-card`)
- For the PerfectDraft Pro side: `Falkvinge/hassio-integration-perfectdraft-pro`

The Blade side works without a smart Blade integration.

## Manual installation

### 1. Install Button Card

Install **Button Card** from HACS and reload/restart Home Assistant if requested.

### 2. Install the artwork

Copy:

`www/perfectdraft/`

to:

`/config/www/perfectdraft/`

Home Assistant exposes this as:

`/local/perfectdraft/`

### 3. Install the Home Assistant package

Copy:

`packages/perfectdraft_on_tap.yaml`

to:

`/config/packages/perfectdraft_on_tap.yaml`

If packages are not already enabled, merge this into your existing `homeassistant:` block:

```yaml
homeassistant:
  packages: !include_dir_named packages
```

Restart Home Assistant after validating configuration.

The package creates the Blade selector, insertion datetime, pint counter, Blade freshness sensor, PerfectDraft selector, PerfectDraft ABV/pints/pours sensors and three Blade automations.

### 4. Configure PerfectDraft Pro

Install and configure the PerfectDraft Pro integration with your own account.

Expected integration entities include:

- `sensor.perfectdraft_pro_temperature`
- `sensor.perfectdraft_pro_keg_remaining`
- `sensor.perfectdraft_pro_keg_freshness`
- `sensor.perfectdraft_pro_pours`
- `sensor.perfectdraft_pro_keg`
- `sensor.perfectdraft_pro_keg_product`
- `button.perfectdraft_pro_mark_keg_changed`

Entity IDs can differ on another installation. See `reference/ENTITY_MAPPING.md`.

### 5. Import the dashboard

Create a new Home Assistant dashboard or view, open the **Raw configuration editor**, and paste the contents of:

`dashboard/on_tap.yaml`

### 6. Select the current kegs

Use:

- `input_select.blade_current_keg`
- `input_select.perfectdraft_current_keg`

Changing the Blade keg automatically stamps the insertion time and resets the Blade counter to 14 pints.

## HACS status

HACS Dashboard repositories require a matching JavaScript file and may ship supporting files from `dist/`. This repository will use that mechanism to distribute the artwork and HACS-specific dashboard assets. The Home Assistant package YAML still needs to be copied/enabled in Home Assistant because HACS Dashboard installs frontend files, not arbitrary Home Assistant helpers and automations.

## Optional theme

Copy `themes/perfectdraft.yaml` to `/config/themes/perfectdraft.yaml`.

For the full theme behaviour, install **card-mod** through HACS.

## Background

The original private uploaded background was deliberately excluded. The dashboard works without it.

## Known ABV limitation

The ABV lookup is preserved from the source configuration and currently covers fewer beers than the full PerfectDraft selector. Some beers may therefore show no ABV until the public lookup is expanded.

## Privacy / sanitisation

The public build removes private IP addresses, account identifiers, Home Assistant uploaded-media IDs, location-specific entity prefixes and other installation-specific values.

## Artwork and trademarks

Beer/product artwork and brand marks remain the property of their respective owners. This repository does not grant redistribution rights to third-party trademarks or artwork.

## Support files

- `QUICK_START.md`
- `reference/ENTITY_MAPPING.md`
- `reference/BUILD_VALIDATION.md`
- `reference/ASSET_MANIFEST.md`

