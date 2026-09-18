# PerfectDraft + Blade Dashboard — Asset Manifest

Complete inventory of the asset package used by the "On Tap" dashboard.
All paths are relative to `/config/www/` (served as `/local/...`).

## A. Package purpose

Public, install-anywhere copy of the image assets referenced by the
PerfectDraft + Blade dashboard (keg artwork, blade machine logos, beer
glass silhouettes and country flags). Extracted only from the dashboard
configuration, the keg-picture automation, and the image directory that
serves them. No private, install-specific, or unrelated files are included.

## B. Directory structure

```
perfectdraft/
├── background/   ← dashboard background image (see section H)
├── blade/        ← 27 logo images for the Blade beer machine
├── flags/        ← 19 country flags
├── glass/        ← 12 beer-glass silhouettes
└── *.png         ← 112 keg artwork images (Beer - On Tap row)
```

## C. File counts

| Location      | Count | Source |
|---------------|-------|--------|
| `background/` | 0 (+README) | supplied separately — see H |
| `blade/`      | 27   | Blade machine logo carousel |
| `flags/`      | 19   | Beer nationality flags |
| `glass/`      | 12   | Glass silhouettes |
| root (*.png)  | 112  | Keg artwork (111 referenced + `neutral-keg-t3.png`) |
| **Total PNG** | **170** | |

## D. Keg artwork (root)

112 PNG files. Naming convention: `<beer>-t3.png` (later |`-t3b`/`-t3c`
variants), with `modelo-especial.png` and `neutral-keg-t3.png` as
non-standard exceptions. Each is the top-down "keg in the PerfectDraft
machine" artwork shown on the "Beer — On Tap" row of the dashboard.

## E. Blade (27)

`affligem-blanche`, `affligem-blonde`, `affligem-fruits-rouges`, `alfa`,
`amstel`, `birra-moretti-baffo-doro`, `birra-moretti-ricetta-originale`,
`brixton-reliance`, `cruzcampo`, `desperados`, `edelweiss-hefetrub`,
`gosser-marzen`, `gosser-zwickl`, `heineken`, `heineken-silver`,
`heineken-zero`, `ladron-de-manzanas`, `lagunitas-ipa`, `linzer-bier`,
`messina-cristalli-di-sale`, `orchard-thieves`, `puntigamer`, `red-stripe`,
`strongbow-dark-fruits`, `tiger`, `villacher-marzen`, `zipfer-urtyp`.
Each maps to a blade keg currently in the machine (carousel of logos).

## F. Glass silhouettes (12)

`alt`, `chalice`, `cider`, `goblet`, `kwak`, `pilsner-flute`, `pint`,
`stange`, `stein`, `tall-pilsner`, `tulip`, `weizen`
→ `glass/<name>-glass.png`. Selected by the glass-type picker on the
"On Tap" beer row.

## G. Flags (19)

`at`, `be`, `cz`, `de`, `es`, `fr`, `gb-eng`, `gb-sct`, `gb-wls`, `gr`,
`ie`, `it`, `jm`, `mx`, `nl`, `se`, `sg`, `th`, `us`
→ `flags/<code>.png`. Selected from the beer's country of origin.

## H. Background (supplied separately — NOT included)

The dashboard background **peakpx.jpg** was not included because the
original currently exists only in Home Assistant's uploaded-media storage
and must be supplied separately.

**To install:** put your chosen background at
`/config/www/perfectdraft/background/peakpx.jpg`
(any filename works — point the dashboard background to it), then set the
dashboard's background image to `/local/perfectdraft/background/...`

## Privacy note

All files are image assets only. No configuration, logs, credentials,
metadata files, or install-specific identifiers are included.