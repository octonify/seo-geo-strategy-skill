# Competitor And Gap Mapping

Owned by [`../SKILL.md`](../SKILL.md) steps 8 and 9.

---

## 1. The competitor set is derived, not asserted

A competitor, for this Skill, is a domain that appeared in an observed SERP for a candidate in this unit's set. Not a domain the client names as a rival, not a domain a model considers similar.

This matters because the client's commercial competitors and the client's search competitors overlap only partly. A practice down the road may be the business rival and hold no relevant SERP position. A directory the client has never thought about may hold four.

Operator-named rivals are still recorded — under `Named by operator`, `User-provided`, with their observed appearance count beside them, which is frequently zero. A zero there is a finding, not an omission.

### Ordering

Rank by appearance count across observed SERPs. Ties break by the number of SERPs where the domain held a top-three position. Both numbers are `Calculated` and both name the SERPs counted.

### Profiling depth

Profile the five highest-appearing domains in full. List the remainder by name with their appearance count only. State the cutoff and the number of domains below it — a silent truncation reads as complete coverage when it is not.

## 2. Competitor profile fields

Per profiled domain:

| Field | Label | Note |
|---|---|---|
| Domain | `Measured` | |
| Result type | `Measured` | From `serp-read-protocol.md` §3 |
| SERPs appeared in | `Calculated` | Name them |
| Top-three appearances | `Calculated` | Name them |
| Best position observed, and where | `Measured` | |
| Ranking URLs observed | `Measured` | The actual URLs, not the domain |
| Page authority / referring domains / backlinks | `Measured` or `Unknown` | Tool and date |
| Page format at the ranking URL | `Measured` or `Unknown` | Service page, article, directory listing, profile |
| Serves this locality | `Measured`, `User-provided`, or `Unknown` | A national institution ranking locally is not a local competitor |
| Named by operator | `User-provided` | Yes / no |

No qualitative verdict column. "Strong content", "weak authority", "beatable" are judgements, and judgements about who to compete with belong to `content-strategy-architect`.

## 3. Coverage segmentation

For each candidate in the set, place it in exactly one segment. Coverage means an observed ranking URL on the domain in question, not a guess about whether a page exists.

| Segment | Condition | Label |
|---|---|---|
| Held | Own site appears in the observed top ten | `Measured` |
| Contested | Own site and at least one competitor both appear | `Measured` |
| Uncovered | Competitors appear, own site does not | `Measured` |
| Open | No comparable local provider appears at all | `Calculated` |
| Unknown | No SERP observed for this candidate | `Unknown` |

`Open` is `Calculated` because it is a statement about absence derived from the result-type counts, and absence is only as good as the observation behind it.

When own-site coverage cannot be established at all — no crawl, no inventory, no sitemap, nothing pasted — every candidate is `Unknown` on the own-site axis, the segmentation runs competitor-to-competitor, and the pack says so in one line. It does not run with own-site coverage assumed absent, which would turn every row into a false `Uncovered`.

## 4. Gap rows

A gap is one row. Every row names the URL that evidences it, on both sides where both exist.

| Field | Label |
|---|---|
| Candidate term | carried from the candidate set |
| Segment | from §3 |
| Competitor URL evidencing coverage | `Measured` |
| Own-site URL, if any | `Measured` or `Unknown` |
| Competitor page format | `Measured` or `Unknown` |
| Demand attached to the term | carried, with its own label |
| Intent class (SERP read) | carried, with its own label |

A gap row with no evidencing URL is not a gap. It is a hypothesis, and it is either dropped or carried explicitly as `Unknown — no evidencing URL observed`.

## 5. Format and question gaps

Two secondary passes, both evidence-bound.

**Format gap.** Across observed SERPs, count which page formats rank and which formats the own site has for this unit. Report as counts per format. The absence of a format is a `Calculated` observation about the observed set, never a claim about the whole web.

**Question gap.** Every People Also Ask question and every AI Overview citation harvested in step 6 is checked against own-site coverage. Unanswered questions are listed verbatim as observed, with the SERP they came from. They are research output — a list of questions with demand evidence. Turning them into headings, and deciding which ones a page should answer, is `content-strategy-architect`'s work, and how they are answered in words is governed by the Skill named in `authority.authority_override_skill`.

## 6. What this step does not produce

No priority score, no tier, no quick-win bucket, no sequencing, no calendar. Every one of those is a decision that ranks candidates against each other, and this Skill produces evidence for that decision rather than making it.

A gap table sorted by observed demand is fine — sorting is a view. A gap table with a `Priority` column is not.
