# Troubleshooting

## Keg image does not appear

Test:

`/hacsfiles/perfectdraft-blade-on-tap/perfectdraft/neutral-keg-t3.png`

If that fails:
- reload HACS
- redownload the repository
- clear the browser/app frontend cache

## "Custom element doesn't exist: button-card"

Install **Button Card** through HACS and reload Home Assistant.

## PerfectDraft values show dashes

Check that the PerfectDraft Pro integration entities exist. The public dashboard expects:

- `sensor.perfectdraft_pro_temperature`
- `sensor.perfectdraft_pro_keg_remaining`
- `sensor.perfectdraft_pro_keg_freshness`
- `sensor.perfectdraft_pro_pours`

If your entity IDs differ, edit the dashboard references.

## ABV shows "ABV —"

The public ABV lookup currently covers fewer beers than the full selector. This is a known limitation of the source data.

## Blade freshness is unavailable

Check:
- `input_datetime.blade_keg_inserted`
- `sensor.blade_keg_freshness`

Changing `input_select.blade_current_keg` should stamp a new insertion time.

## Configuration errors after adding the package

If this Home Assistant installation already had the same helpers/entities, remove the duplicate package. Do not define the same YAML helper/template twice.

## Dashboard loads but artwork is blank after an update

Force refresh the browser/app frontend. HACS assets can be cached.

## Theme fonts do not load

The optional theme imports Google Fonts and may be blocked by DNS/content filtering. The dashboard falls back to local/common fonts.
