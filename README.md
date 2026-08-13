# Post-Show Analytics — Design Prototype

An interactive design prototype for a live-selling post-show analytics experience.
Single self-contained HTML file — no build step, no dependencies, no network calls.

**Open `index.html` in any browser.**

## Surfaces

| Surface | What it does |
|---|---|
| **Overview** | Account-level, organised as four questions in funnel order — *How did I do? → Who bought from me? → Where did they come from? → What should I fix?* — with a sticky section rail |
| **Shows** | A sortable list of every show, configurable columns, CSV export |
| **Show dashboard** | Per-show recap: headline GMV with an auction / Buy Now split, a 16-metric key-data grid, a minute-by-minute run of show, and per-show breakdowns |

## The metric explorer

The main Overview chart is a general-purpose plotter rather than a fixed chart. Pick
any of 16 metrics, optionally a second to compare, a breakdown dimension, a time
grain (day / week / month / show), and a comparison period.

Chart form is **derived from the selection** rather than being another dropdown:

| Selection | Rendered as |
|---|---|
| One metric | Line + area |
| One metric + breakdown | Stacked bars, with a Value ⇄ Share % toggle |
| Two metrics, same unit | Two lines on one axis |
| Two metrics, different units | Two panels on a shared x-axis |

That last row is deliberate. Two mismatched units on a single plot with two y-scales
invents a correlation that isn't in the data, so that state is unreachable by design.
Breakdown and second-metric are mutually exclusive for the same reason — both would
need the colour channel.

## Run of show

The per-show timeline plots any two of six per-minute series, across three time
windows (whole show / last 30 min / last 5 min). Event markers use a single colour
with the type carried by **shape** — ● pinned item, ◆ giveaway, ■ promotion — so they
never collide with a series colour. Clicking the chart jumps the replay to that
moment.

## Design notes

- **Single light theme**, painted explicitly rather than inheriting the host page.
- **The chart palette is validated, not eyeballed.** Series colours clear OKLab
  colour-vision-deficiency separation (ΔE ≥ 8 under simulated protanopia and
  deuteranopia), a normal-vision floor of ΔE ≥ 15, and a lightness/chroma band
  against the page surface. Breakdowns cap at five series because that is where the
  palette stops clearing the gate. Two series sit below 3:1 contrast, so every chart
  also ships direct value labels — colour is never the only encoding.
- **Every chart has a table view and an export.** Tooltips enhance; they never gate
  access to a value.

## Data

**All data is fabricated.** The seller, shows, buyers, items and every figure are
invented for demonstration purposes. No real customer, seller or transaction data
appears anywhere in this file.

## Status

Design prototype only — not production code, and not wired to any data source.
