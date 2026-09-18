# ENTITY_MAPPING.md

Every entity the **On Tap** dashboard expects and where it comes from.
The names below are the public, installation-neutral names used by this package.

## A. Blade entities

| Entity | Kind | Created by |
|---|---|---|
| `input_select.blade_current_keg` | helper | `helpers.yaml` |
| `input_datetime.blade_keg_inserted` | helper | `helpers.yaml` |
| `counter.blade_pints_remaining` | helper | `helpers.yaml` |
| `sensor.blade_keg_freshness` | template sensor | `templates.yaml` |

### Blade automations

| Automation ID | Logic |
|---|---|
| `blade_keg_change_stamp_inserted` | Keg selection changes → stamp `input_datetime.blade_keg_inserted` |
| `blade_keg_change_reset_pints` | Keg selection changes → reset `counter.blade_pints_remaining` to 14 |
| `blade_pints_daily_decrement` | Daily at 00:00 → decrement the Blade counter by 1 |

## B. PerfectDraft entities

| Entity | Kind | Created by |
|---|---|---|
| `input_select.perfectdraft_current_keg` | helper | `helpers.yaml` |
| `input_number.pours_keg_start` | helper | `helpers.yaml` |
| `sensor.perfectdraft_current_keg_abv` | template sensor | `templates.yaml` |
| `sensor.perfectdraft_pints_remaining` | template sensor | `templates.yaml` |
| `sensor.perfectdraft_pours_this_keg` | template sensor | `templates.yaml` |
| `sensor.perfectdraft_pro_temperature` | integration sensor | PerfectDraft integration |
| `sensor.perfectdraft_pro_keg_remaining` | integration sensor | PerfectDraft integration |
| `sensor.perfectdraft_pro_keg_freshness` | integration sensor | PerfectDraft integration |
| `sensor.perfectdraft_pro_pours` | integration sensor | PerfectDraft integration |
| `sensor.perfectdraft_pro_keg` | integration sensor | PerfectDraft integration |
| `sensor.perfectdraft_pro_keg_product` | integration sensor | PerfectDraft integration |
| `button.perfectdraft_pro_mark_keg_changed` | integration button | PerfectDraft integration |

### Data flow

```text
Blade dropdown
  ├─> inserted datetime ─> Blade freshness
  └─> Blade pint counter

PerfectDraft integration
  ├─> keg remaining % ─> PerfectDraft pints remaining
  ├─> raw pours ─> pours this keg
  ├─> temperature
  └─> keg freshness

PerfectDraft dropdown ─> current keg ABV
```

## Entity-ID note

Home Assistant entity IDs can differ if a device or entity has previously been
renamed. The dashboard supplied with this package uses the generic names above.
If an integration-created entity has a different ID on another installation,
map that installation's entity to the corresponding dashboard reference.
