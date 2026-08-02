# Internal Link Map

Owned by [`../SKILL.md`](../SKILL.md) step 9. What links are required inside a cluster, what a link row carries, and the line between a link decision and a wording decision.

---

## 1. The required links

A cluster is not a set of pages that happen to be about one topic. It is a set of pages wired together, and the wiring is what the architecture actually delivers.

| Link | Required | Why |
|---|---|---|
| Pillar → every member | Yes, one per member | The pillar is what makes the members findable as a set |
| Every member → pillar | Yes, exactly one per member | Bidirectional linking is what marks the group as one body of work rather than scattered pages |
| Member ↔ member | Only where evidenced | See §3 |
| Retired page → its owner | Yes, for every `retire` disposition | So the inbound signal has somewhere to go |

`Done when` item 12 checks the first two mechanically: every member has at least one row with the pillar as target and one with the pillar as source.

**No quota.** There is no target number of links per page here. Published averages exist and vary by source; none of them is a measurement of this cluster, and applying one would put an unlabelled number into a decision. What is checked is the required wiring and whether each target resolves.

---

## 2. What a row carries

```
| Source page | Target page | Target concept | Target resolves? | Label      |
|-------------|-------------|----------------|------------------|------------|
| <page-1>    | <page-2>    | <concept>      | Yes — <url>      | Measured   |
| <page-2>    | <page-1>    | <concept>      | Yes — <url>      | Measured   |
| <page-1>    | <page-3>    | <concept>      | Not yet — in map | Calculated |
| <page-4>    | <page-1>    | <concept>      | Unknown          | Unknown    |
```

| Cell | What it holds |
|---|---|
| Source page | A page in this cluster map, or an existing page in the inventory |
| Target page | The same |
| **Target concept** | What the link is *about* — the idea the reader is being sent to. Structural |
| Target resolves? | `Yes — <url>` for a confirmed existing URL; `Not yet — in map` for a page this run defines; `Unknown` where neither could be confirmed |
| Label | `Measured` for a confirmed URL, `Calculated` for a target defined in this map, `Unknown` otherwise |

**A row whose target is `Unknown` is a defect**, listed as one. Recommending a link to a page nobody can confirm exists is how broken internal links get planned deliberately.

**No row names an unresolved target.** Every target is either an existing URL from the inventory or a page in the Cluster Map. A target that is neither is not written into the map at all — it is recorded as a finding.

---

## 3. Cross-links between members

A member-to-member link is added only when the evidence shows a reason:

| Reason | Evidence that supports it |
|---|---|
| The two terms share a meaningful part of their SERP without meeting the merge threshold | The overlap count from `cannibalization-guardrails.md` §2, in the 1–3 band |
| One page's boundary sentence explicitly hands a sub-topic to the other | The Cluster Map's boundary column |
| The pack recorded an unanswered question on one page's SERP that the other page answers | The pack's unanswered-questions list, quoted with its source |

Cross-links with no reason from this list are not added. "These feel related" produces the dense, undifferentiated linking that makes a cluster's shape unreadable.

---

## 4. The wording boundary

**This file decides link targets. It never decides anchor text.**

| Decided here | Decided by the Skill in `authority.authority_override_skill` |
|---|---|
| Which page links to which | The words in the anchor |
| The target concept the link is about | Whether the anchor is a phrase, a clause, or part of a sentence |
| That the anchor should describe its target rather than be a bare pointer | How specific the description is, and how strong any claim inside it is |
| Which pages must be reachable from which | The sentence the link sits inside |

The structural principle that a link should describe where it goes is a link-graph property and belongs here. The words that do the describing are language and do not. A link map that ships with suggested anchor phrases has already crossed the line, however good the phrases are, and policy kernel §1 has no exception for a measurable gain.

Practically: the brief carries `Target concept: <concept>` and the writer produces the anchor. The record never carries a column headed `Anchor text` or `Suggested anchor`.

---

## 5. What this file does not decide

- **Navigation, header, footer, breadcrumb.** Sitewide structure, not one cluster.
- **URL taxonomy across the site.** The brief names a URL pattern only where this cluster's own parentage requires one.
- **Orphan sweeps and link audits across the whole site.** A different unit and a different completion criterion.
- **Redirects.** A redirect is a change to a live object (policy kernel §1). The map records that a retired page's inbound links belong to the owner; the consuming project's implementation Skill decides and performs anything live.
- **Link counts as a score.** No structure score, no /100. `docs/decisions.md` D12's reasoning — a composite over mixed-quality inputs carries no honest label — applies to structure scores exactly as it applied to keyword scores.
