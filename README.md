# Tide

A dependency-free progressive web app for Delta 20 wave training: barbell deadlift, bench and squat plus a kettlebell clean & press day, each built from moderate sets with heavy sets placed between them, plus density blocks and SkiErg conditioning. Data lives in the browser's localStorage; the service worker caches everything for offline use.

## The program

Four sessions per wave week, on any days. "Next up" follows this order but skips squat the day after deadlift (and the reverse).

| # | Session |
|---|---|
| 1 | Deadlift → pull-ups + floor push-ups density → SkiErg 20 min easy |
| 2 | Bench press → skull crushers + curls density → SkiErg intervals |
| 3 | Squat → SkiErg 35 min easy |
| 4 | Kettlebell clean & press → ring rows + curls density → SkiErg intervals |

**Block:** 4, 8 or 12 weeks, built from 4-week cycles. Weekly volume follows the Soviet ratios 15 / 22 / 28 / 35% in these orders:

| Cycle | Weeks | Order (1 = lightest) | Multiplier |
|---|---|---|---|
| Intro | 1–4 | 1, 2, 3, 4 | ×1.0 |
| Load | 5–8 | 1, 3, 4, 2 | ×1.2 |
| Taper | 9–12 | 3, 4, 2, 1 | ×1.44 |

A 4-week block is Intro; 8 weeks adds Load; 12 weeks adds Taper. Volume resets at the end of each block.

**Across the week:** volume (INOL) is split deadlift 15%, squat 22%, bench 28%, clean & press 35%. Each lift's heavy share uses the same ratios inverted: 35, 28, 22, 15%. The volume level is set by bench's peak-week INOL (default 1.7); every lift scales with it. If your heavy-set e1RM hasn't risen by the end of a block, raise it 0.2; if you aren't recovering, lower it 0.2.

**Within a session:**
- Moderate sets at 75% of e1RM (kettlebell: double 53s, % from max reps via the NSCA table).
- Heavy sets between them: barbell at 85 → 87 → 90 → 92% across each 4-week cycle, at least 2 heavy sets per barbell lift every week; kettlebell single-arm 70 lb.
- Every set is a third to two-thirds of the reps possible at its weight (75%: 4–6; 85%: 2–4; 87%: 2–3; 90%: 2; 92%: 1–2).
- Back-to-back moderate sets differ by at least 20% (for example 6, 4, 6, 4), and each lift's total reps change by at least 20% from week to week, following the wave's direction.
- Loads round half-up to 5 lb. Training max is 90% of 1RM by default.

**Stops:** bench and squat moderate sets run on a fixed interval (2:00 / 2:30) and stop after any set whose fastest rep is more than 15% slower than set 1's (adjustable). Deadlift and kettlebell sets stop above RPE 8. A rated heavy set (reps and RPE) estimates e1RM and offers to update it.

**Readiness tiers:** Full; Reduced (about 20% fewer moderate reps, one heavy set, easy SkiErg); Minimum (one heavy set at RPE ≤ 7, nothing else). Full and Reduced count toward the wave; Minimum counts if the heavy set is done.

**SkiErg intervals:** 30 s hard / 60 s easy, by feel. Rounds mirror the lifting wave: each week takes the opposite volume rank (heaviest lifting week = fewest rounds, lightest = most), with no +20% per cycle, because the effort is self-regulated and fitness shows up as more watts at the same effort. The week's rounds are split 56% bench day / 44% clean & press day; each day's rounds change at least 20% week to week, and the clean & press day stays at least 20% below the bench day. Default weekly peak 22 rounds: bench day 5–12 rounds, clean & press day 4–10, about 8 minutes of hard work a week on average. Intervals always come after the lifts. Average watts can be logged for each session.

**Week advancement:** not tied to the calendar. The wave advances once all four sessions of the current week are counted. "Skip to next week" forces it.

**Progression at the end of a block:** a heavy single at 92% or more at RPE ≤ 8 adds 5 lb (bench) or 10 lb (squat, deadlift) to e1RM. If every 70 lb set in the last week was done at RPE ≤ 7, its max reps rises by one. Density pairs add load when a 10-minute total reaches 120% of baseline.

**Upgrading from v1:** training maxes, velocity stop, bar weight, body log, density baselines and old session logs carry over; the wave starts at block 1, week 1.

## Deploy

Push to GitHub and enable Pages (Settings → Pages → deploy from branch, root). Bump `VERSION` in `sw.js` with every release so installed copies update.
