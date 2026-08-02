# Observation Label Map

Owned by [`../SKILL.md`](../SKILL.md), applied at every step that records what a
source says.

`references/policy-kernel.md` §2 defines the five labels. This file does one
thing the kernel does not: it fixes, per class of local-presence observation,
which labels are permitted, which are forbidden, and what must travel alongside
the value. It adds no label and changes no definition.

---

## 1. The map

| Observation | Permitted | Forbidden | Must carry |
|---|---|---|---|
| A NAP string read off a surface | `Measured`, `Unknown` | `Estimated` | The surface, the date, and how it was observed |
| A NAP string the operator supplied with no surface named | `User-provided`, `Unknown` | `Measured` | Who supplied it and when |
| A canonical NAP field read from config | `User-provided` | `Measured` | The config key it came from |
| A canonical NAP field adopted from an observed source | `Measured` | `Estimated` | The source adopted, its surface, and its date |
| A comparison of two strings | `Calculated`, `Unknown` | `Measured` | Both strings quoted in full, and which two sources they came from |
| A GBP checklist item's state | `Measured`, `Unknown` | `Estimated`, `Calculated` | The surface, the date, and how it was observed |
| A citation listing's presence | `Measured`, `Unknown` | `Estimated` | The listing URL, the date checked |
| A citation listing's absence | `Measured`, `Unknown` | `Estimated`, `Calculated` | The date checked and the search performed. **Absence is only `Measured` when a check was actually run** |
| A source not checked | `Unknown` | everything else | The reason it was not checked |
| A dated observation carried in from an earlier session | `Measured`, `User-provided` | `Estimated` | Its original date, its original surface, who observed it, and the words `not re-observed this run` |
| Counts across the tables | `Calculated`, `Unknown` | `Measured` | Which rows were counted |
| An existing page URL | `Measured`, `Unknown` | `Estimated` | How its existence was confirmed |
| A locality to be served | `User-provided`, `Unknown` | `Measured`, `Estimated` | Who named it |
| A guideline a profile is checked against | `Measured`, `Unknown` | `Estimated` | The documentation source and the date it was read |
| Local-pack presence for a term | `Measured`, `Unknown` | `Estimated` | Carried in from a `seo-geo-research` pack with the pack's own label, surface and date, unchanged |

## 2. The source list, in observation order

Observed in this order because each step's result changes what the next one
means. The site is read first because it is the business's own most-controlled
statement about itself; the profile second because it is the highest-weight
third-party surface; the directories last because a variance there is only
interpretable once the first two are known.

| # | Source | What is read | Notes |
|---|---|---|---|
| 1 | The live site at `site.canonical_host` | Every place the site states the business name, address, or phone | **Each place is its own row.** A footer, a contact page, and a location page can disagree with each other, and a single site-level row would hide it |
| 2 | The Google Business Profile named by `local_presence.gbp_profile_name` | The name, address and phone as published, plus every checklist item | Observed from an operator export, a dashboard screenshot, or the public listing. Never by signing in |
| 3–n | Each source in [`citation-sources.md`](citation-sources.md) §2, in tier order | The name, address and phone as published, and the listing URL | A source not reached is `Unknown — not checked`, and the reason is recorded |

Where the site publishes structured markup carrying a NAP, that markup is read
as its own row alongside the visible text on the same page. Markup and visible
text disagreeing is a finding; deciding what the markup should say is
`content-strategy-architect`'s schema decision, not this Skill's.

## 3. The four rules that generate the map

1. **A string is transcribed, never normalised.** Record what the surface says,
   character for character, including case, punctuation, abbreviation and
   ordering. Normalising on the way in destroys the difference the run exists to
   find.

2. **A comparison is `Calculated` and shows both inputs.** It is not relabelled
   as one of its inputs, and a comparison against a string that was never
   observed is `Unknown`, not a pass.

3. **Absence is only observable by looking.** `missing` means a check was run
   and the listing was not there. `Unknown — not checked` means no check was
   run. Collapsing the two turns a to-do list into a false audit.

   The same rule applied to time: an observation is evidence about **its own
   date** and about no other. A string read four days ago is carried with that
   date and the words `not re-observed this run`, and the source's current state
   goes in the Unknowns table. It is neither presented as current nor thrown
   away — discarding the only observation there is leaves the comparison unmade,
   which is a worse answer than a dated one.

4. **No local-presence observation is ever `Estimated`.** Every value in this
   Skill's record is a string somebody published or a comparison between two
   such strings. There is nothing here for a model to infer, and a label that
   permits inference would let an unobserved directory be described.

This is **stricter than policy kernel §2**, which permits `Estimated` for model
inference generally. It narrows the permitted set for one class of observation;
it adds no label and contradicts nothing. The same reasoning already applies to
SERP composition in `docs/decisions.md` D13.

## 4. The evidence-basis count

The handoff summary carries
`Evidence basis: n Measured, n User-provided, n Calculated, n Estimated, n Unknown`.

Count every labelled value in the record, once each, under the label it carries.
**What counts as one labelled value is defined once, for all three Skills, in
[`../../../references/skill-contract.md`](../../../references/skill-contract.md) §5.**
Apply that rule; do not define a counting rule for this run.

`Calculated` is counted as itself. On a well-formed run of this Skill the
`Estimated` count is `0`; a non-zero count is a defect, not a variation, and
`Done when` item 16 surfaces it by requiring the counts to match the record.

## 5. What this record is not

It is a flat, dated snapshot of one location's presence: three canonical strings,
a checklist, a status per source, and a page plan.

It is **not** an event log, an append-only stream, a projection rebuilt from
revisions, or a multi-principal identity store. `docs/decisions.md` D4 studied
and rejected that machinery for this bundle: it exists to reconcile contested
identity across a large organisation, and a single location's NAP is not
contested in that way — it is simply written down in several places, some of
them out of date.

The practical consequence is that a run supersedes the previous run rather than
appending to it. Where history matters, the previous record is the history, and
it is read as a document.
