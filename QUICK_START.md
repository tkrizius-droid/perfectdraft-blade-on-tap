# Quick start

## HACS route

1. Install **HACS**, **Button Card** and **Expander Card** (`Alia5/lovelace-expander-card`).
2. In HACS, add `tkrizius-droid/perfectdraft-blade-on-tap` as a **Dashboard** custom repository.
3. Download **PerfectDraft + Blade On Tap**.
4. Copy `packages/perfectdraft_on_tap.yaml` from this GitHub repository to `/config/packages/` and enable Home Assistant packages if needed.
5. For PerfectDraft Pro, install/configure `Falkvinge/hassio-integration-perfectdraft-pro`.
6. Import `dashboard/on_tap_hacs.yaml` into a Home Assistant dashboard Raw configuration editor.
7. Select your current Blade and/or PerfectDraft keg.

## Manual route

Copy `www/perfectdraft/` to `/config/www/perfectdraft/`, copy the package YAML as above, then import `dashboard/on_tap.yaml`.

See `README.md` for the full instructions, entity mapping and troubleshooting.
