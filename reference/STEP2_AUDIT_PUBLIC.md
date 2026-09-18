# STEP2_AUDIT_PUBLIC.md
# Step 2 audit — PerfectDraft + Blade support entities

This is the public-safe version of the Step 2 audit. Account identifiers,
device-registry identifiers, local network details, source automation IDs and
other installation-specific metadata have been intentionally excluded.

## PerfectDraft integration

The dashboard expects a PerfectDraft Home Assistant integration that supplies
temperature, keg remaining percentage, keg freshness, raw pour count, keg name,
keg product and the mark-keg-changed button.

The integration itself is not bundled here. Users should install and configure
their own compatible PerfectDraft integration and must never share its account
credentials or Home Assistant config-entry data.

## Blade helpers

The Blade side is manual and uses:

- `input_select.blade_current_keg`
- `input_datetime.blade_keg_inserted`
- `counter.blade_pints_remaining`

Selecting a new Blade keg stamps the insertion datetime and resets the counter
to 14. A daily automation decrements the counter by one; dashboard +/- buttons
allow manual correction.

## Blade freshness

`sensor.blade_keg_freshness` counts down from 30 days using
`input_datetime.blade_keg_inserted`, never below zero.

## PerfectDraft derived sensors

`sensor.perfectdraft_pints_remaining`:
```jinja
{{ (states('sensor.perfectdraft_pro_keg_remaining') | float(0) / 100 * 10.5) | round(1) }}
```

`sensor.perfectdraft_pours_this_keg`:
```jinja
{{ states('sensor.perfectdraft_pro_pours') | int(0) - states('input_number.pours_keg_start') | int(0) }}
```

`sensor.perfectdraft_current_keg_abv` uses the beer-name-to-ABV lookup contained
in `templates.yaml`. Its values are intentionally preserved from the supplied
working configuration at this stage.

## Important ABV coverage note

The PerfectDraft dropdown contains more beers than the current ABV lookup.
Beers missing from the lookup return no ABV value. The supplied lookup also
contains a duplicate key and one likely legacy/mistyped beer-name key. These
have deliberately not been changed during Step 2.

## Files safe to share at this stage

- `helpers.yaml`
- `templates.yaml`
- `automations.yaml`
- `perfectdraft.yaml`
- `ENTITY_MAPPING.md`
- `README_STEP2.md`
- `STEP2_AUDIT_PUBLIC.md`
- `perfectdraft_dashboard_step2.yaml`

Beer/keg artwork is not part of Step 2 and will be packaged separately.
