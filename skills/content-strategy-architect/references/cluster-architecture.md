# Cluster Architecture

Owned by [`../SKILL.md`](../SKILL.md) steps 5 and 7. Page roles, the boundary rule, the member-count guidance, and aggregate cluster demand.

---

## 1. Roles

A cluster has exactly one pillar and one or more members. Every page carries one role, one owning term, one boundary sentence, and one disposition.

| Role | What it is | How many |
|---|---|---|
| `pillar` | The page that owns the cluster's broadest term and links to every member | Exactly one |
| `member` | A page owning one narrower term inside the pillar's topic | One or more |
| `entry` | A member whose SERP-read intent is provider-seeking and whose local pack is present — flagged for `local-presence-manager`, architected here | Zero or more |

**Disposition** is separate from role and is one of:

| Disposition | Meaning | Consequence |
|---|---|---|
| `create` | No page exists for this term | A brief is produced |
| `extend` | A page exists and will absorb this term | A brief is produced, naming the existing URL |
| `keep` | A page exists, owns its term, needs nothing from this run | No brief |
| `retire` | A page exists and should stop competing | No brief; the link map routes its inbound links to the owning page |

`retire` is a recommendation about page ownership. It is never executed here — nothing in this bundle changes a live page (policy kernel §1).

---

## 2. The boundary sentence

Every page in the map carries **one sentence** stating what it covers and what it hands to a sibling.

```
<page> covers <what it owns>; <what it does not cover> is handled by <sibling page>.
```

This is the cheapest cannibalization control there is, and it is a `Done when` item because a boundary that only exists in the architect's head does not survive the handoff. Two pages whose boundary sentences do not name each other are two pages that will drift into the same query.

The sentence states scope, not wording. `<page> covers <sub-topic>` is structural. `<page> reassures anxious readers that…` is language and belongs to the Skill in `authority.authority_override_skill`.

### Member-count guidance

Current external guidance on topic-cluster architecture converges on fewer, deeper clusters over more, thinner ones, with supporting-page counts commonly quoted in the high single digits to low tens per pillar.

**It is guidance and it is treated as guidance.** The published figures vary widely between sources and are not tied to any measurement this bundle can reproduce, so:

- No page is invented to reach a count.
- No page is cut to stay under one.
- A cluster outside the range proceeds, with the count stated (continue-silently gate 4).

What the count is actually for: a one-member cluster is a page, not a cluster, and should be recorded as such rather than dressed as an architecture. A thirty-member cluster is usually two clusters that were never separated, and the overlap counts in `cannibalization-guardrails.md` §2 will normally show where the seam is.

---

## 3. Aggregate cluster demand

**This is an addition to the methodology, not a codification of past practice** (`docs/decisions.md` D9). It is labelled as an addition wherever it appears, per the D9 pattern, so a later session does not mistake it for inherited precedent.

### The rule

Evaluate demand across the whole cluster, not only per term. A cluster of eight terms that are individually thin can be a stronger proposition than one term with a larger number, and per-term reading cannot see that.

### The arithmetic, and its honesty problem

Summing demand across members runs directly into policy kernel §2: an `Unknown` member has no value, and giving it one to complete the sum is the "`Unknown` silently becomes zero" failure the kernel names.

So the aggregate is reported as a **floor**, never as a total:

```
Cluster demand (local): floor 340 across 5 of 9 members — Calculated
  <term-a> 120 (Measured, <tool>, <locality>, <date>)
  <term-b>  90 (Measured, <tool>, <locality>, <date>)
  <term-c>  60 (Measured, <tool>, <locality>, <date>)
  <term-d>  40 (Measured, <tool>, <locality>, <date>)
  <term-e>  30 (Measured, <tool>, <locality>, <date>)
  Unknown members: 4 — <term-f>, <term-g>, <term-h>, <term-i>
  This is a floor. The true aggregate is at least this and is not known.
  (Aggregate cluster demand is an addition — docs/decisions.md D9)
```

Rules:

- The word `floor` appears whenever any member is `Unknown`. `Done when` item 6.
- The `Unknown` members are named, not just counted.
- When **every** member is `Unknown`, the line reads `Unknown — no member carries a demand value`, and there is no floor. A floor of zero would be a claim.
- Local and national aggregates are reported separately, on the markets the pack read them at. They are never added together.

### What the aggregate is used for, and what it is not

Used for: stating the size of the proposition in the record, and for the brief's context section so the writer knows whether this is a cluster with observed demand or a cluster being built on intent evidence alone.

**Not used for:** ranking this cluster against another cluster, sequencing which page gets written first, or producing a score. Sequencing is not this bundle's decision, and a composite score built from a mix of `Measured` and `Unknown` inputs carries no honest label — the same reasoning that rejected every scoring model in `docs/decisions.md` D12 applies unchanged here.

---

## 4. Assembling the map

1. The primary keyword chosen in step 6 is the pillar's owning term.
2. Every member of the overlap grouping that is not the pillar's own group becomes a candidate member page.
3. Each candidate member is checked against the existing inventory: a term an existing page already owns is `extend` or triggers stop-and-ask gate 7, never a new page.
4. Every page gets its boundary sentence, naming at least one sibling.
5. Terms marked `held` in step 4 — those whose SERP was not observed — appear in the map with disposition blank and a `Unknown` note, never as `create`. A page is not created on unobserved evidence.

```
| Page       | Role   | Owns term | Boundary sentence | Disposition | Existing URL |
|------------|--------|-----------|-------------------|-------------|--------------|
| <page-1>   | pillar | <term-a>  | <sentence>        | extend      | <url>        |
| <page-2>   | member | <term-b>  | <sentence>        | create      | none — to be created |
| <page-3>   | member | <term-c>  | <sentence>        | keep        | <url>        |
| <page-4>   | member | <term-d>  | <sentence>        | —           | none — held, SERP not observed |
```

---

## 5. What this file does not decide

Page format beyond the role, word count, section order inside a page, heading wording, and the reading level of anything are not decided here. Sub-intent in the pack names a format; the brief carries the format and the required sections; the Skill in `authority.authority_override_skill` writes them.

Whole-site information architecture — navigation, URL taxonomy across sections, breadcrumb design, sitewide crawl depth — is not this unit. This Skill architects one cluster. A URL pattern is recorded in the brief only where the cluster's own parentage requires one, and the consuming project's implementation Skill owns what is actually built.
