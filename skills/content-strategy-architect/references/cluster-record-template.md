# Cluster Architecture Record Template

Owned by [`../SKILL.md`](../SKILL.md) step 13. `SKILL.md` `## Output` carries the compact skeleton; this file carries the full form, filled in literally.

Placeholders in `<angle brackets>` are replaced. Everything else is written as shown. A section with nothing to report is kept and filled with `none` or `Unknown — <reason>`. Sections are never dropped for being empty.

---

```markdown
# Cluster Architecture — <cluster> — <YYYY-MM-DD>

Decisions with their evidence trail. Produced by content-strategy-architect
from one seo-geo-research evidence pack. All language on every page named here
is owned by <authority.authority_override_skill>.

## Inputs

| Config key | Value used | Label |
|---|---|---|
| client.id | <value> | User-provided |
| client.display_name | <value> | User-provided |
| authority.authority_override_skill | <value> | User-provided |
| site.canonical_host | <value> | User-provided |
| site.cms | <value> | User-provided |
| site.seo_plugin | <value> | User-provided |
| market.primary_locality | <value> | User-provided |
| market.national_dataset | <value> | User-provided |
| market.language | <value> | User-provided |
| planning_record.path | <value> | User-provided |
| planning_record.owned_fields | <value> | User-provided |
| planning_record.row_identifier_field | <value> | User-provided |
| constraints.excluded_topics | <value or "not set"> | User-provided |
| constraints.held_topics | <value or "not set"> | User-provided |
| constraints.retired_services | <value or "not set"> | User-provided |
| outputs.content-strategy-architect.path | <value or "not set"> | User-provided |

Missing required keys: <list, or "none">
Output file written to: <path, or "none — emitted in session only">

## Pack provenance

| Field | Value |
|---|---|
| Pack unit | <unit the pack was run on> |
| Pack run date | <YYYY-MM-DD> |
| Pack status | complete / partial / stopped |
| Pack open questions carried forward | <list, or "none"> |

Fields this Skill needed that the pack does not carry: <list, or "none">
Each is a finding about the pack, not a metric produced here.

## Inherited decisions

One row per page already existing in this cluster. If none exists, this table
reads `none — no existing page in this cluster`.

| Existing page | Declared primary | Snapshot date | Snapshot source | Rejected alternatives recorded at | Label |
|---|---|---|---|---|---|
| <page> | <term or Unknown — reason> | <date or Unknown — reason> | <source or Unknown — reason> | <where or Unknown — reason> | <label> |

## Re-verification defects

Written every run. Every Inherited-decisions row carrying `Unknown` in its
snapshot-date or snapshot-source cell appears here. When none qualifies, this
section reads `none`.

| Page | What is missing | Consequence |
|---|---|---|
| <page> | <what> | <what cannot now be established, stated plainly> |

What would resolve each: <a fresh seo-geo-research run on that page's topic,
or the named artifact that would carry the snapshot>

## Cluster membership

Overlap threshold: <the rule, stated as a sentence>

| Candidate | Overlap count | SERPs counted | Verdict | Label |
|---|---|---|---|---|
| <term> | <n or —> | <the two reads, or which was not observed> | member / held / excluded | Calculated / Unknown |

Candidates in the pack: <n> · members: <n> · held: <n> · excluded: <n>

## Cluster demand

Local: <floor <n> across <n> of <n> members — Calculated, or "Unknown — no member carries a demand value">
  <one line per member counted, with its value, label, source, market, date>
  Unknown members: <n> — <named>
National: <same shape>

Aggregate cluster demand is an addition to the methodology, not codified past
practice — docs/decisions.md D9. Local and national are never added together.

## Primary keyword

Recommended: <term>

| Metric | Value | Label | Source | Market | Date |
|---|---|---|---|---|---|
| Local volume | <value> | <label> | <source> | <locality> | <date> |
| National volume | <value> | <label> | <source> | <dataset> | <date> |
| Tool difficulty | <value> | <label> | <source> | <market> | <date> |
| Intent (SERP read) | <value> | <label> | <surface> | <locality> | <date> |
| Coverage segment | <value> | <label> | <surface> | <locality> | <date> |
| Local pack present | <value> | <label> | <surface> | <locality> | <date> |

### Rejected alternatives

At least two rows, always.

| Term | Why it lost | Value that decided it | Label |
|---|---|---|---|
| <term> | <reason> | <the observed value> | <label> |
| <term> | <reason> | <the observed value> | <label> |

### Selection rationale

| # | Criterion | What it showed | Decided it? |
|---|---|---|---|
| 1 | SERP-read intent match | <what was observed> | <yes/no> |
| 2 | Brand contamination | <what was observed> | <yes/no> |
| 3 | Coverage segment | <what was observed> | <yes/no> |
| 4 | Observed difficulty | <what was observed> | <yes/no> |
| 5 | Demand | <what was observed> | <yes/no> |
| 6 | Local pack presence | <what was observed> | <yes/no> |

Criteria that were Unknown for all candidates: <list, or "none">

## Cluster map

| Page | Role | Owns term | Boundary sentence | Disposition | Existing URL |
|---|---|---|---|---|---|
| <page> | pillar / member / entry | <term> | <one sentence naming a sibling> | create / extend / keep / retire / — | <url or "none — to be created"> |

Pages flagged for local-presence-manager: <list, or "none">

## Term ownership

| Primary term | Owning page | Conflicts found |
|---|---|---|
| <term> | <page> | <finding, or "none"> |

Own-site coverage established by: <method, or "Unknown — not established in the pack">
Where Unknown, every `create` disposition above is provisional on that check.

## Link map

| Source page | Target page | Target concept | Target resolves? | Label |
|---|---|---|---|---|
| <page> | <page> | <concept> | Yes — <url> / Not yet — in map / Unknown | <label> |

Required links present: pillar → every member <n/n> · every member → pillar <n/n>
Rows with an Unknown target: <n> — each is a defect, listed above
No column headed anchor text appears in this table, by design.

## Schema decisions

| Page | Type | Documented rich result | Docs read on | Visible content it maps to |
|---|---|---|---|---|
| <page> | <type> | yes / no — entity value only / Unknown | <date> | <content> |

Types already emitted by <site.seo_plugin>: <list, or "none / Unknown">

## Briefs

One per page with disposition `create` or `extend`, each filled from
references/content-brief-template.md, each carrying its own exclusion check.

<briefs, in cluster-map order>

## Record writes

| Row identifier | Field | Prior value | New value | Written on | By |
|---|---|---|---|---|---|
| <identifier> | <field> | <prior or "(empty)"> | <new> | <date> | content-strategy-architect |

Identifier field used: <planning_record.row_identifier_field>
Rows created: <n> · rows updated: <n> · writes stopped: <n>
Owned fields not written, and why: <list, or "none">

## Unknowns

Every `Unknown` in this record, with what would resolve it.

| What is unknown | Where it appears | What would resolve it |
|---|---|---|

## Done-when check

| # | Item | Pass/Fail | Evidence |
|---|---|---|---|
| 1 | <item text from SKILL.md> | <Pass/Fail> | <where to look> |

<... one row per item, all sixteen, every run ...>

Overall: <complete / partial / stopped>

### Handoff summary

- **Skill:** content-strategy-architect
- **Unit:** <the cluster>
- **Status:** complete | partial | stopped
- **Produced:** <record path or "in-session record only">, <n> briefs, <n> planning rows written
- **Evidence basis:** <n> Measured, <n> User-provided, <n> Calculated, <n> Estimated, <n> Unknown
- **Assumptions:** <each assumption made without asking, or "none">
- **Open questions:** <each unresolved item, or "none">
- **Recommended next:** <authority.authority_override_skill> | local-presence-manager | return to operator
```

---

## Notes on filling it in

**The Done-when check table is written every run, in full, pass or fail.** Sixteen rows appear whether sixteen pass or four do. A checklist that is only written when the agent remembers to write it is documentation, not enforcement (`references/skill-contract.md` §4).

**The Re-verification defects section is written even when it is empty.** It is the section that makes an existing cluster's undocumented decisions visible, and a section that only appears when it has content cannot be relied on to appear.

**A label is never upgraded in transit.** A value the pack labelled `Estimated` is `Estimated` here. A value the pack labelled `Unknown` stays `Unknown`; this Skill has no way to resolve it and no licence to produce it (`docs/decisions.md` D11 gives the metrics to the research Skill, and that boundary holds in both directions).

**`Status: partial` is a legitimate outcome.** A record that names a primary keyword, three defects it cannot resolve, and a planning write it stopped is more useful than one that filled the gaps with plausible numbers.
