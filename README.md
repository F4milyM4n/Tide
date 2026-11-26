# Tide

A dependency-free progressive web app for a three-week wave training block: barbell top sets with velocity-based back-offs, kettlebell clean & press EMOMs, density blocks, and SkiErg conditioning. Data lives in the browser's localStorage; the service worker caches everything for offline use.

## The program

Four sessions per wave week, on any days. "Next up" follows this order but skips squat the day after deadlift (and the reverse).

| # | Session |
|---|---|
| 1 | Deadlift → pull-ups + floor push-ups density → SkiErg 20 min easy |
| 2 | Bench press → skull crushers + curls density → SkiErg intervals |
| 3 | Squat → SkiErg 35 min easy |
| 4 | Kettlebell clean & press EMOM → ring rows + curls density → SkiErg intervals |

**Barbell wave** (percent of estimated 1RM; training max = 90% of 1RM by default; loads round half-up to 5 lb)

| Week | Top set | Back-offs (maximum) |
|---|---|---|
| 1 Accumulation | 5 @ 79% (RPE 7) | 4 × 6 @ 65% |
| 2 Transmutation | 3 @ 86% (RPE 8) | 5 × 4 @ 70% |
| 3 Realization | 1–2 @ 91% (RPE 8) | 4 × 3 @ 75% |

- Squat and bench back-offs run on a fixed interval (2:30 / 2:00) with a velocity stop: the last set is the first whose fastest rep is more than 10% slower than set 1's.
- Deadlift back-offs use full rest and stop above RPE 8; velocity is logged for trends only.
- Top-set velocity ≥ 0.05 m/s below the last session at the same week suggests the Reduced tier.

**Readiness tiers:** Full; Reduced (1 back-off, 6-minute density, easy SkiErg); Minimum (top set at RPE ≤ 7 only, or a 10-minute EMOM). Full and Reduced count toward the wave; Minimum counts if the top set (or any EMOM minute) is done.

**Week advancement:** not tied to the calendar. The wave advances once all four sessions of the current week are counted, however many days that takes. "Skip to next week" forces it.

**Progression after week 3:** a top single at RPE ≤ 8 at or above target adds 5 lb (bench) or 10 lb (squat, deadlift) to e1RM. One kettlebell week per cycle gains a rep per minute if all 20 minutes were completed with the last at RPE ≤ 7; at the cap, move up a bell in Setup. Density pairs add load when a 10-minute total reaches 120% of baseline.

## Deploy

Push to GitHub and enable Pages (Settings → Pages → deploy from branch, root). Bump `VERSION` in `sw.js` with every release so installed copies update.
