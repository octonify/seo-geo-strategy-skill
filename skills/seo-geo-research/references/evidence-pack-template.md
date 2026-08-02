# Evidence Pack Template

Owned by [`../SKILL.md`](../SKILL.md) step 11. `SKILL.md` `## Output` carries the compact skeleton; this file carries the full form, filled in literally.

Placeholders in `<angle brackets>` are replaced. Everything else is written as shown. A section with nothing to report is kept and filled with `None observed` or `Unknown — <reason>`. Sections are never dropped for being empty.

---

```markdown
# Keyword And SERP Evidence — <unit> — <YYYY-MM-DD>

Research pack. Contains labelled evidence and no recommendation.
Target selection, cluster design, and page ownership are decided by
content-strategy-architect from this pack.

## Inputs

| Config key | Value used | Label |
|---|---|---|
| client.id | <value> | User-provided |
| client.display_name | <value> | User-provided |
| authority.authority_override_skill | <value> | User-provided |
| site.canonical_host | <value> | User-provided |
| market.primary_locality | <value> | User-provided |
| market.national_dataset | <value> | User-provided |
| market.language | <value> | User-provided |
| research_tools.available | <value> | User-provided |
| research_tools.access_mode | <value> | User-provided |
| constraints.excluded_topics | <value or "not set"> | User-provided |
| constraints.held_topics | <value or "not set"> | User-provided |
| constraints.retired_services | <value or "not set"> | User-provided |
| outputs.seo-geo-research.path | <value or "not set"> | User-provided |

Missing required keys: <list, or "none">
Output file written to: <path, or "none — emitted in session only">

## Universe

Sources that ran: <list by number and name from keyword-universe-sources.md §1>
Sources that did not run, and why: <list, or "none">
Terms in universe: <n>
Terms carried to candidate set: <n>
Screening rule applied: <the rule, stated>
Terms discarded: <n>

<Universe table — Term | Source | Label at discovery | Notes>

## Candidates

Every row carries every column. An unavailable value is `Unknown` with a
reason in the same cell. No cell is blank and no cell is 0 by default.

| Term | Local volume | National volume | Tool KD | Intent (query) | Intent (SERP) | Disagree | Evidence |
|---|---|---|---|---|---|---|---|
| <term> | <n or Unknown — reason> | <n or Unknown — reason> | <n or Unknown> | <class · sub-intent> | <class or Unknown — not observed> | <Yes/No> | <tool, market, date> |

Local metrics read at: <market.primary_locality>
National metrics read at: <market.national_dataset>
Tool, and date of reading: <tool>, <date>
Device: <desktop/mobile, or Unknown>

## SERP reads

One block per candidate with an observed SERP. Candidates without one are
listed at the end of this section as `Unknown — not observed`.

### <term>

Surface: <surface> · Locality: <locality> · Device: <device> · Date: <date>

Features present: <ticked list>
Features absent: <ticked list>
Features not checked: <list — these are Unknown, not absent>

| Pos | URL | Domain | Result type | Page authority | Ref domains | Backlinks |
|---|---|---|---|---|---|---|

Result-type mix: <counts> — Calculated
People Also Ask questions observed: <verbatim list, or "none">
AI Overview sources cited: <list, or "not present" / "not checked">

Findings fired: <named findings from serp-read-protocol.md §5, or "none">

Observed difficulty:

| Input | Value | Label |
|---|---|---|
| Top-ten authority spread | <values> | Measured |
| Referring domains spread | <values> | Measured |
| Result-type mix | <counts> | Calculated |
| Content bar | <what ranks> | Measured |
| Feature pressure | <features> | Measured |
| Tool difficulty score | <value, tool, market, date> | Measured |
| Divergence from tool score | <yes/no + direction> | Calculated |

Read: <one sentence describing the SERP. No "should", no "recommend",
       no ranking against another candidate.>

## Competitors

Profiled in full: <n> · Listed by name only: <n> · Cutoff rule: <stated>

| Domain | Result type | SERPs appeared in | Top-3 appearances | Best position | Ranking URLs | Authority | Serves locality | Named by operator |
|---|---|---|---|---|---|---|---|---|

Named by operator but not observed in any SERP: <list, or "none">

## Coverage and gaps

Own-site coverage established by: <method, or "Unknown — not established">

| Term | Segment | Competitor URL | Own-site URL | Competitor format | Demand | Intent (SERP) |
|---|---|---|---|---|---|---|

Format gap (observed set only): <counts per format>
Unanswered questions with observed demand: <verbatim list, or "none">

## GEO surfaces

| Term | AI Overview | Sources cited | PAA | Video | Local pack | Label |
|---|---|---|---|---|---|---|

## Unknowns

Every `Unknown` in this pack, with what would resolve it.

| What is unknown | Where it appears | What would resolve it |
|---|---|---|

## Done-when check

| # | Item | Pass/Fail | Evidence |
|---|---|---|---|
| 1 | <item text from SKILL.md> | <Pass/Fail> | <where to look> |

<... one row per item, all of them, every run ...>

Overall: <complete / partial / stopped>

### Handoff summary

- **Skill:** seo-geo-research
- **Unit:** <unit>
- **Status:** complete | partial | stopped
- **Produced:** <artifact paths, or "in-session pack only">
- **Evidence basis:** <n> Measured, <n> User-provided, <n> Calculated, <n> Estimated, <n> Unknown
- **Assumptions:** <each assumption made without asking, or "none">
- **Open questions:** <each unresolved item, or "none">
- **Recommended next:** content-strategy-architect | return to operator
```

---

## Notes on filling it in

**The Done-when check table is written every run, in full, pass or fail.** A checklist that is only written when the agent remembers to write it is documentation, not enforcement (`references/skill-contract.md` §4). Twelve rows appear whether twelve pass or three do.

**`Unknown` rows are the point of the Unknowns section, not an embarrassment.** A pack with eleven `Unknown` cells and a clear statement of what would resolve each is more useful to the next Skill than a pack with eleven confident numbers of unstated origin.

**Nothing in the pack names a target.** If a filled pack contains a sentence recommending a keyword, a page, or a cluster, the pack is wrong regardless of how good the recommendation is — the receiving Skill needs the evidence unprejudiced, and the decision trail required by `references/policy-kernel.md` §3 is built there, not here.
