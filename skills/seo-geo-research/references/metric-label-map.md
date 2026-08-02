# Metric Label Map

Owned by [`../SKILL.md`](../SKILL.md), applied at every step that produces a number.

`references/policy-kernel.md` §2 defines the five labels. This file does one thing the kernel does not: it fixes, per research metric, which labels are permitted, which are forbidden, and what must travel alongside the value. It adds no label and changes no definition.

---

## 1. The map

| Metric | Permitted | Forbidden | Must carry |
|---|---|---|---|
| Local search volume | `Measured`, `Calculated`, `Unknown` | `Estimated` as a bare number | Tool, locality, date. `Calculated` shows both inputs and their labels. |
| National search volume | `Measured`, `User-provided`, `Unknown` | `Estimated` | Tool, dataset, date |
| Tool keyword difficulty | `Measured`, `Unknown` | `Estimated`, `Calculated` | Tool, market, date, and the scale it is on |
| Observed difficulty inputs | `Measured`, `Calculated`, `Unknown` | `Estimated` | Surface, locality, date |
| CPC | `Measured`, `Unknown` | `Estimated` | Tool, market, date, currency |
| Competitive density | `Measured`, `Unknown` | `Estimated` | Tool, market, date |
| Intent from query pattern | `Estimated` | `Measured` | Nothing — it is inference and is labelled as such |
| Intent from SERP | `Measured`, `Unknown` | `Estimated` | Surface, locality, date, and the features that evidence it |
| SERP feature presence | `Measured`, `Unknown` | `Estimated`, `Calculated` | Surface, locality, date |
| Ranking URL and domain | `Measured`, `Unknown` | everything else | Position, surface, date |
| Page authority, referring domains, backlinks | `Measured`, `Unknown` | `Estimated` | Tool, date |
| Result-type mix | `Calculated`, `Unknown` | `Measured` | The rows counted |
| Competitor SERP-appearance count | `Calculated`, `Unknown` | `Estimated` | Which SERPs were counted |
| Own-site coverage | `Measured`, `User-provided`, `Unknown` | `Estimated` | How coverage was established |
| Content gap | `Calculated`, `Unknown` | `Measured` | The evidencing URL on both sides |
| AI Overview citation | `Measured`, `Unknown` | `Estimated` | Surface, locality, date |
| Term source at discovery | `Measured`, `User-provided`, `Estimated` | — | Which of the eight sources |

## 2. The four rules that generate the map

1. **Anything read off a surface is `Measured`, and carries the surface, the market, and the date.** A volume without a market and a date is not evidence (policy kernel §2). Tools disagree with each other and each tool's own figures move over time, so the reading is only reproducible if it is stamped.

2. **Anything derived arithmetically is `Calculated` and shows its inputs with their own labels.** It is not relabelled as one of its inputs. A derivation from an `Estimated` input is no stronger than that input, and showing the inputs is what makes that visible — a reader judges the derivation from the inputs on the page, not from a label that has absorbed them.

3. **Model inference is `Estimated` and never sits in a column that a reader will scan as a measurement.** The query-pattern intent read is the one place `Estimated` belongs, because the pack shows the SERP-read column beside it.

4. **Absent is `Unknown` with a reason, never zero, never a default, never a blank cell.**

## 3. The zero-volume rule

A keyword tool reporting `0` for a locality is reporting that it has no data for that locality. It is not reporting that nobody searches the term.

Small-market and geo-modified queries routinely return zero from tools that carry real national volume for the same phrase. Recording that zero as a demand figure would let a real candidate be discarded on a data-coverage artifact.

Therefore, when a tool reports local volume as `0`:

```
Local volume:    Unknown — tool reports 0 for <locality>, <tool>, <date>
National volume: <n> — Measured, <tool>, <dataset>, <date>
```

Both lines always appear together. The national figure is the cross-check that shows whether the term has demand at all.

### The population-ratio figure

A local figure may be derived as `national volume × (locality population ÷ dataset population)`.

It is permitted only as:

```
Local volume (derived): <n> — Calculated
  national volume <n> (Measured, <tool>, <dataset>, <date>)
  × locality population <n> (User-provided or Measured, <source>, <date>)
  ÷ dataset population <n> (User-provided or Measured, <source>, <date>)
  Not a substitute for a measured local volume.
```

It never replaces the `Unknown` line, never appears without its inputs, and never appears in a column headed as a measurement. Both population inputs must themselves be labelled; if either is missing, the derived figure is not produced at all.

## 4. The evidence-basis count

The handoff summary carries `Evidence basis: n Measured, n User-provided, n Calculated, n Estimated, n Unknown`.

Count every labelled value in the pack, once each, under the label it carries. **What counts as one labelled value is defined once, for all three Skills, in [`../../../references/skill-contract.md`](../../../references/skill-contract.md) §5.** Apply that rule; do not define a counting rule for this run, and do not state one beside the totals. Two operators applying two rules to the same pack both report `Pass` and mean different things.

`Calculated` is counted as itself — it is one of the five labels in policy kernel §2 and gets its own count. The counts must sum to the number of labelled values in the pack — this is a `Done when` item and is checked by counting, not by judgement.
