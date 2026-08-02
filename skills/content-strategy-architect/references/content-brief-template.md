# Content Brief Template

Owned by [`../SKILL.md`](../SKILL.md) step 11. One brief per page whose disposition is `create` or `extend`.

Placeholders in `<angle brackets>` are replaced. Everything else is written as shown. A section with nothing to report is kept and filled with `none` or `Unknown — <reason>`. Sections are never dropped for being empty.

**The brief carries structure, evidence, and constraints. It carries no language.** §3 below is the check that this held.

---

## 1. The template

```markdown
# Brief — <page> — <YYYY-MM-DD>

Structural brief. All wording is decided by <authority.authority_override_skill>.
This brief states what must be true of the page, never how anything is phrased.

## Placement

| Field | Value |
|---|---|
| Cluster | <cluster> |
| Role | pillar / member / entry |
| Disposition | create / extend |
| Existing URL | <url, or "none — to be created"> |
| Parent page | <pillar, or "this is the pillar"> |
| Language | <market.language> |
| Locality the evidence was read at | <market.primary_locality> |

## Ownership

Primary term this page owns: <term>
Boundary: <the one boundary sentence from the Cluster Map>
Sibling pages named in that boundary: <list>
Terms this page must NOT be built to own: <list of sibling primaries>

## Evidence behind the target

| Metric | Value | Label | Source | Market | Date |
|---|---|---|---|---|---|
| Local volume | <n or Unknown — reason> | <label> | <source> | <locality> | <date> |
| National volume | <n or Unknown — reason> | <label> | <source> | <dataset> | <date> |
| Intent (SERP read) | <class · sub-intent> | <label> | <surface> | <locality> | <date> |
| Coverage segment | <segment> | <label> | <surface> | <locality> | <date> |
| Observed difficulty | <the inputs, separately> | <label> | <surface> | <locality> | <date> |

Rejected alternatives are recorded at: <where in the cluster record>
Cluster demand context: <the floor line, with its Unknown count>
Criteria that were Unknown for all candidates: <list, or "none">

## Format the evidence calls for

Sub-intent observed: <sub-intent>
Format that sub-intent implies: <format>
Local pack present on this term's SERP: <yes / no / Unknown>
Result types occupying the observed top ten: <the mix>

## Required sections

Heading level and topic only. The wording of every heading is decided by
<authority.authority_override_skill>.

| Level | Topic the section must cover | Why it is required | Label |
|---|---|---|---|
| H2 | <topic> | <the observed evidence that requires it> | <label> |
| H2 | <topic> | <the observed evidence that requires it> | <label> |
| H3 | <topic> | <the observed evidence that requires it> | <label> |

## Questions the page must answer

Observed on the SERP and carried verbatim as data, with their source. Whether
any of these becomes a heading, and in what words, is decided by
<authority.authority_override_skill>.

| Question as observed | Where observed | Date | Label |
|---|---|---|---|
| <question> | <surface, locality> | <date> | Measured |

## Proof obligations

What the page must be able to support, not how it is said.

| Claim area the page will need to stand behind | What must be cited | Who supplies it |
|---|---|---|
| <area> | <the kind of source required> | <operator / client / Unknown> |

## Structural requirements for machine legibility

| Requirement | Status |
|---|---|
| The page's clearest answer to its main question appears near the top | Required |
| Heading hierarchy reflects the actual structure of the content | Required |
| Each section is readable without its neighbours | Required |
| Deliberate fragmentation of content for machine extraction | Recorded disagreement — see cluster record; not required |

## Internal links

Links out of this page:

| Target page | Target concept | Target resolves? |
|---|---|---|
| <page> | <concept> | <Yes — url / Not yet — in map> |

Links into this page, to be added on the source pages:

| Source page | Target concept | Source resolves? |
|---|---|---|
| <page> | <concept> | <Yes — url / Not yet — in map> |

No anchor wording appears in either table, by design.

## Schema

| Type | Documented rich result | Docs read on | Visible content it must correspond to |
|---|---|---|---|
| <type> | <yes / no — entity value only> | <date> | <content> |

What this markup will do: <plain statement. Where the rich-result cell is "no",
this line says that no rich result follows from it.>
Already emitted by <site.seo_plugin>: <yes — confirm, do not duplicate / no / Unknown>

## Owned by <authority.authority_override_skill>, not decided here

Every item below is named so the writer knows it is theirs, and so nobody
looks for it in this brief and assumes it was forgotten.

- Title tag and meta description — wording, in full
- H1 and every heading — wording, in full
- All body copy
- Every anchor phrase for the links above
- Claim strength, specificity, and outcome phrasing
- CTA presence, placement, and framing
- Tone, register, and reading level
- Any compliance or safety constraint on the above

## Constraints read from configuration

| Constraint | Value | Effect on this page |
|---|---|---|
| constraints.excluded_topics | <value or "not set"> | <effect, or "none"> |
| constraints.held_topics | <value or "not set"> | <effect, or "none"> |
| constraints.retired_services | <value or "not set"> | <effect, or "none"> |

## Unknowns carried into this brief

| What is unknown | Where it affects the page | What would resolve it |
|---|---|---|

## Exclusion check

| # | Excluded from this brief | Present? |
|---|---|---|
| 1 | A sentence of body copy | <no / FAIL> |
| 2 | A headline or heading wording | <no / FAIL> |
| 3 | A title tag or meta description | <no / FAIL> |
| 4 | An anchor phrase | <no / FAIL> |
| 5 | A CTA wording | <no / FAIL> |
| 6 | A claim phrased as it would appear on the page | <no / FAIL> |
| 7 | A word-count target | <no / FAIL> |
| 8 | A tone, voice, or register instruction | <no / FAIL> |
```

---

## 2. Notes on filling it in

**Every required section names the evidence that requires it.** A section in the brief with no observed reason behind it is a section somebody imagined. The acceptable reasons are: a result type or format observed in the top ten, an unanswered question observed on the SERP with demand behind it, a gap row from the pack naming a competitor URL, or a boundary handoff from a sibling page.

**The observed questions are data, not drafting.** They are strings read off a SERP and carried with their source and date, exactly as the pack carried them. Quoting them is evidence discipline. Turning one into a heading is a language decision and is not made here.

**Word count is excluded deliberately.** It is a proxy for depth that constrains the writer without carrying any evidence, and the Skill that owns the writing is better placed to judge it. Where the observed top ten shows a content bar, the brief states what the ranking pages actually contain — which is an observation — rather than converting it into a number to hit.

**An `extend` brief names what already exists.** The existing URL, the sections the page already has, and which required sections are new. Otherwise the writer cannot tell an addition from a rewrite, and a rewrite of a page that was working is a real cost.

---

## 3. The exclusion check is the point

The check table is written every run, all eight rows, whether they pass or not. A brief with a `FAIL` row is not emitted — it is corrected first.

This is enforcement rather than advice because the pressure runs one way. Every reason to slip across the line sounds constructive at the time: the phrasing is obvious, the writer will only ask, one example makes the section clearer. `CLAUDE.md` and policy kernel §1 both settle it — the client's voice Skill outranks this bundle on all language, and there is no SEO or GEO gain that justifies overriding a client's safety layer. A brief that hands over "just a starting point" for a claim has overridden it, whatever the intent.
