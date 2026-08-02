# Local Presence Record Template

Owned by [`../SKILL.md`](../SKILL.md) step 9. `SKILL.md` `## Output` carries the
compact skeleton; this file carries the full form, filled in literally.

Placeholders in `<angle brackets>` are replaced. Everything else is written as
shown. A section with nothing to report is kept and filled with `none` or
`Unknown — <reason>`. Sections are never dropped for being empty.

---

```markdown
# Local Presence — <location> — <YYYY-MM-DD>

Observed state and recommendations. Nothing in this record has been performed:
no profile was edited, no listing submitted, no page changed, nothing spent.
All language fields named below are owned by <authority.authority_override_skill>.

Run type: complete run | observation-only run (stop-and-ask gate 2, option 3)

## Inputs

| Config key | Value used | Label |
|---|---|---|
| client.id | <value> | User-provided |
| client.display_name | <value> | User-provided |
| authority.authority_override_skill | <value> | User-provided |
| site.canonical_host | <value> | User-provided |
| market.primary_locality | <value> | User-provided |
| market.language | <value> | User-provided |
| local_presence.gbp_profile_name | <value or "missing"> | User-provided |
| local_presence.canonical_nap.name | <value or "missing"> | User-provided |
| local_presence.canonical_nap.address | <value or "missing"> | User-provided |
| local_presence.canonical_nap.phone | <value or "missing"> | User-provided |
| local_presence.service_area_mode | <value or "missing"> | User-provided |
| constraints.excluded_topics | <value or "not set"> | User-provided |
| constraints.retired_services | <value or "not set"> | User-provided |

Missing required keys: <list, or "none">
seo-geo-research pack supplied: <path or "none — optional input not supplied">
Output file written to: <path, or "none — emitted in session only">

## Observed sources

Every string below is transcribed exactly as the surface presents it: case,
punctuation, abbreviation and ordering unchanged. Nothing is normalised.

| # | Source | Surface | Observed on | How observed | Name string | Address string | Phone string | Label |
|---|---|---|---|---|---|---|---|---|
| 1 | Site — <page role> | <URL> | <YYYY-MM-DD> | <browser read / operator paste / screenshot> | <exact string> | <exact string> | <exact string> | Measured |
| 2 | Site — <page role> | <URL> | <YYYY-MM-DD> | <method> | <exact string> | <exact string> | <exact string> | Measured |
| 3 | Google Business Profile | <listing URL or place identifier> | <YYYY-MM-DD> | <method> | <exact string> | <exact string> | <exact string> | Measured |
| n | <citation source> | <listing URL or "none found"> | <YYYY-MM-DD or "—"> | <method or "not checked"> | <exact string or "Unknown — not checked"> | <…> | <…> | Measured / Unknown |

Sources observed: <n> · sources not checked: <n>
Site places carrying NAP: <n> — <list the page roles>
Rows carried from an earlier session: <n> — each reads
`as at <YYYY-MM-DD>, not re-observed this run` in its "How observed" cell, and
its current state appears in the Unknowns table

## Canonical NAP

One exact string per field, agreed once.

| Field | Canonical value | Origin | Label |
|---|---|---|---|
| Name | <exact string, or "Unknown — not agreed"> | <config key / observed source + date> | User-provided / Measured / Unknown |
| Address | <exact string, or "Unknown — not agreed"> | <config key / observed source + date> | User-provided / Measured / Unknown |
| Phone | <exact string, or "Unknown — not agreed"> | <config key / observed source + date> | User-provided / Measured / Unknown |

Gate taken at step 3: <none / gate 2 option n / gate 3 option n / gate 4 option n>

## NAP variance

Compared against: <the canonical> — or, on an observation-only run:
`Comparison base: <source>, observed <YYYY-MM-DD>. This is a base for
comparison, not a canonical. No canonical was agreed.`

| # | Source | Field | Base string | Observed string | Class | What is identical underneath | Label |
|---|---|---|---|---|---|---|---|
| 1 | <source> | Name / Address / Phone | <full string> | <full string> | digits-differ / words-differ / format-only | <for format-only rows; "—" otherwise> | Calculated |

Sources compared: <n> · not checked: <n> · differing: <n>
First-party disagreement (site versus profile): <yes — name the field and both
strings / no / Unknown — one side not observed>

## Format decisions

| Choice | Chosen form | Sources carrying it | Sources carrying another form |
|---|---|---|---|
| <e.g. suite designator> | <chosen, or "Unknown — not agreed"> | <list> | <list, with the form each carries> |

Contested choices: <n, or "none">

## GBP checklist

Guideline documentation read on: <YYYY-MM-DD>, from <source> — or
`not read this run; every guideline-dependent item is Unknown`

| # | Item | Status | Observed value | Observed on | How observed | Label |
|---|---|---|---|---|---|---|
| 1 | Profile identified | <status> | <listing URL or place identifier> | <date> | <method> | Measured / Unknown |
| 2 | Verification state | <status> | <observed indicator> | <date> | <method> | Measured / Unknown |
| 3 | Name field | <status> | <exact published string> | <date> | <method> | Measured / Unknown |
| 4 | Address, published or hidden | <status> | <exact published string, or "hidden"> | <date> | <method> | Measured / Unknown |
| 5 | Service areas | <status> | <list as published> | <date> | <method> | Measured / Unknown |
| 6 | Primary category | <status> | <exact string> | <date> | <method> | Measured / Unknown |
| 7 | Additional categories | <status> | <exact strings, count> | <date> | <method> | Measured / Unknown |
| 8 | Phone | <status> | <exact published string> | <date> | <method> | Measured / Unknown |
| 9 | Website URL | <status> | <URL, and the host it resolves to> | <date> | <method> | Measured / Unknown |
| 10 | Hours | <status> | <as published, incl. seasonal> | <date> | <method> | Measured / Unknown |
| 11 | Description | <status> | present / absent · length <n> characters | <date> | <method> | Measured / Unknown |
| 12 | Photos | <status> | count <n> · most recent observed <date or Unknown> | <date> | <method> | Measured / Unknown |
| 13 | Services or products list | <status> | count <n> | <date> | <method> | Measured / Unknown |

Every `present-wrong` row above quotes the observed value and names the value it
disagrees with. Wording is not assessed anywhere in this table.

## Citations

| Tier | Source | Status | Listing URL | Checked on | Searches run | Label |
|---|---|---|---|---|---|---|
| 1 | Google Business Profile | <status> | <URL> | <date> | <n> | Measured / Unknown |
| 2 | <source> | <status> | <URL or "none found">| <date or "—"> | <n or "—"> | Measured / Unknown |
| 5 | <vertical directory, named by operator> | <status> | <URL or "not named"> | <date or "—"> | <n or "—"> | Measured / Unknown |

Checked: <n> · not checked: <n> · present with variance: <n> · rows: <n>
Duplicate listings observed: <n — name the sources, or "none">

## Page plan

Pattern from `local_presence.service_area_mode`: <value>

| # | Page | Type | Owns locality | Disposition | Existing URL | Must carry |
|---|---|---|---|---|---|---|
| 1 | <page> | location / service-area | <one locality> | create / extend / keep / retire / Unknown | <URL or "none — to be created"> | <elements, per location-page-plan.md §1> |

Localities planned: <n> · localities named but not planned, and why: <list or "none">
Handed to content-strategy-architect for term ownership, cluster role, links and
schema: <yes / no — with reason>

## Remediation

Every row is a recommendation. None has been performed.

| # | Target | Observed state | Recommended end state | Performed by |
|---|---|---|---|---|
| 1 | <source or surface> | <what was observed> | <what it should say> | <operator / named role> |

Rows: <n> · ordered by the tier of the source affected.

## Language fields and their owner

Named, never drafted here.

| Field | Where it appears | Owner |
|---|---|---|
| Business description | GBP checklist item 11 | <authority.authority_override_skill> |
| Location and service-area page copy | Page plan | <authority.authority_override_skill> |
| Page titles, headings, calls to action | Page plan | <authority.authority_override_skill> |

## Unknowns

| What is unknown | Where it appears | What would resolve it |
|---|---|---|
| <e.g. status of <n> citation sources> | Citations | <a check of each named source> |

## Assumptions stated under continue-silently

| # | Gate | Assumption applied |
|---|---|---|
| 1 | <gate number and name> | <what was assumed> |

## Done-when check

One row per item in `SKILL.md` `Skill Contract`, every run, whether it passes or
not.

| # | Item | Pass/Fail/n-a | Evidence |
|---|---|---|---|
| 1 | First line names location and date; Inputs table complete | <Pass/Fail> | <where to look> |
| 2 | Observed Sources table complete; the live site is a row | <Pass/Fail> | <where to look> |
| 3 | Canonical NAP holds one value per field, labelled, with origin | <Pass/Fail/n-a> | <where to look> |
| 4 | NAP Variance table quotes both strings for every differing source, and names what it compared against | <Pass/Fail> | <where to look> |
| 5 | Every variance row classified; format-only rows state what is identical | <Pass/Fail> | <where to look> |
| 6 | Format Decisions table complete, or "none" | <Pass/Fail> | <where to look> |
| 7 | Thirteen GBP rows, each with a status, date and method | <Pass/Fail> | <where to look> |
| 8 | Every present-wrong GBP row quotes the observed value | <Pass/Fail> | <where to look> |
| 9 | One citation row per source; no unchecked source marked missing | <Pass/Fail> | <where to look> |
| 10 | Three citation counts stated; statuses sum to the row count | <Pass/Fail> | <where to look> |
| 11 | Page Plan complete; no locality on two rows | <Pass/Fail/n-a> | <where to look> |
| 12 | Service-area mode publishes no address and no map | <Pass/Fail/n-a> | <where to look> |
| 13 | Remediation rows name a performer; nothing performed here | <Pass/Fail> | <where to look> |
| 14 | No drafted description, copy, headline, title, meta or CTA | <Pass/Fail> | <where to look> |
| 15 | Every Measured value carries surface, date and method | <Pass/Fail> | <where to look> |
| 16 | This table has sixteen rows; evidence-basis counts match the record | <Pass/Fail> | <where to look> |

### Handoff summary

- **Skill:** local-presence-manager
- **Unit:** <the one business location>
- **Status:** complete | partial | stopped
- **Produced:** <record path or "in-session record only">, <n> page plan rows, <n> remediation rows
- **Evidence basis:** <n> Measured, <n> User-provided, <n> Calculated, <n> Estimated, <n> Unknown
- **Assumptions:** <each assumption made without asking, or "none">
- **Open questions:** <each unresolved item, or "none">
- **Recommended next:** content-strategy-architect | <authority.authority_override_skill> | return to operator
```

---

## Filling rules

1. **Every table is written, every run.** An empty one carries `none` or
   `Unknown — <reason>` and stays in place. A dropped section makes a thin run
   look like a clean one.
2. **Strings are quoted in full, never summarised.** "Differs slightly" is not a
   finding. Both strings, in full, in the same row.
3. **`Estimated` should not appear anywhere.** Every value here is a published
   string or a comparison of two of them
   ([`observation-label-map.md`](observation-label-map.md) §3, rule 4). A
   non-zero `Estimated` count is a defect to report, not a variation to accept.
4. **The Done-when table has exactly sixteen rows.** `n/a — observation-only
   run` is permitted on items **3, 11 and 12 only**, and only when stop-and-ask
   gate 2 option 3 was taken; the run type at the head of the record must say
   so. Items 4, 5 and 6 are never `n/a` — the comparison between observed
   sources needs no canonical, and on an observation-only run it is the whole
   result.
5. **A carried observation states its own date.** A row observed in an earlier
   session reads `as at <YYYY-MM-DD>, not re-observed this run`, and the
   source's current state appears in the Unknowns table.
6. **Nothing in the record is phrased as an action taken.** Past tense belongs
   to observations. Recommendations are written as end states with a performer
   named.
