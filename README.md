# Cairn

**Next action, not the whole mountain.**

A self-contained, browser-only productivity tool. Tell it how much time you have and what your energy is like; it picks one activity and times the block.

No account. No network. No install. Open `index.html` directly — everything lives in your browser (or in the JSON you export).

## How it works

Three tabs:

- **Decide** — pick your available time (15 – 120 min) and energy (low / medium / high), then press Decide. Cairn draws a weighted activity that fits the time window and energy requirement, corrected for what you've under-done over the last 7 days. You get two rerolls if you push back.
- **Calibration** — 7-day view of actual vs intended time-share per activity, plus block count, total hours, and bail rate. Dashed marker = target; filled bar = what you actually did.
- **Setup** — add/edit activities: name, weight (relative priority), min/max block length, energy level, and time-of-day window. Export as `cairn.json` to back up or git-track your config.

## The algorithm

Activities are sampled proportionally to weight, then tilted by the gap between intended and actual share over the last 7 days:

```
adjusted_weight = weight × (1 + K × (intended − actual) / intended)
```

`K` defaults to 1. A back-to-back repeat of the same activity is gently penalised. Nothing fancier.

## Usage

```
open index.html
```

- **Space** to decide or start a block (when not focused in a text field)
- **Export / Import** under Setup to back up data as `cairn.json`
- Data persists in `localStorage` under the key `cairn.v1`

## Visual design

Uses the [Tunnel aesthetic](https://github.com/nihilisticiconoclast/cuddly-lamp) — chart-paper palette, Fraunces / Public Sans / IBM Plex Mono type, hard edges, contour-map signature.
