# Primary Keyword Selection

Owned by [`../SKILL.md`](../SKILL.md) steps 2 and 6. This file carries the criteria, the mandatory evidence trail, the rule for deciding when evidence is `Unknown`, and the re-verification pass on decisions inherited from earlier work.

---

## 1. What a primary keyword is here

The one term a page is built to own. Exactly one page in the cluster owns it (`cannibalization-guardrails.md` §3), and it is the term the page's evidence trail is about.

It is not the only term the page may rank for, it is not a phrase anyone has to write into a sentence, and it is not a wording decision. It is an ownership decision, and the Skill named in `authority.authority_override_skill` decides how — or whether — the term ever appears in prose.

---

## 2. The criteria, applied in this order

Order matters. The first criterion that separates the candidates decides, and the rationale names which one did.

| # | Criterion | Read from | Why it sits here |
|---|---|---|---|
| 1 | **SERP-read intent matches the page this cluster needs** | The pack's Pass B intent column | The engine's decision about the query, not a model's opinion of it. A term whose SERP is answering a different question cannot be owned by this page at any volume |
| 2 | **The SERP is not brand-contaminated** | The pack's findings, brand-contamination check | A term whose top results are one entity's own properties is that entity's term. Ranking for it is a different project |
| 3 | **Coverage segment** | The pack's Held / Contested / Uncovered / Open / Unknown column | `Uncovered` and `Open` are where a new page changes something. `Held` usually means extend an existing page, not build a new one |
| 4 | **Observed difficulty inputs** | The pack's per-candidate difficulty inputs, read separately | Read as inputs, never as one score. A thin, outdated or directory-filled top ten is a different proposition from a tool score that says the same number |
| 5 | **Demand** | The pack's local and national volume columns, with their labels | Last, deliberately. A low-demand term with owned intent beats a high-demand term whose SERP is answering something else |
| 6 | **Local-pack presence** | The pack's GEO surfaces table | Where present, it is the strongest signal the engine reads the query as provider-seeking. Flag the page for `local-presence-manager`; do not act on it here |

**Demand is criterion 5, not criterion 1.** Selecting on volume first discards terms whose intent is exactly right before their intent is ever read. External guidance is consistent on this and it is the same argument the pack makes by refusing to rank candidates for us.

**Criterion 1 is a gate, not a weight.** A candidate that fails it is not a weaker candidate; it is not a candidate. Record it in the rejected table with intent as the reason.

---

## 3. The evidence trail — mandatory

`docs/decisions.md` D8. A primary-keyword recommendation is **incomplete** without both of the following. This is enforced by `SKILL.md` `Done when` items 7 and 8, not left to judgement.

### 3.1 The dated metric snapshot

Every value behind the decision, frozen at the date it was read. A trail that points at a live tool is not a trail — the tool's numbers move.

```
| Metric               | Value              | Label        | Source   | Market      | Date         |
|----------------------|--------------------|--------------|----------|-------------|--------------|
| Local volume         | <n> or Unknown — … | Measured     | <tool>   | <locality>  | <YYYY-MM-DD> |
| National volume      | <n> or Unknown — … | Measured     | <tool>   | <dataset>   | <YYYY-MM-DD> |
| Tool difficulty      | <n> or Unknown     | Measured     | <tool>   | <market>    | <YYYY-MM-DD> |
| Intent (SERP read)   | <class · sub>      | Measured     | <surface>| <locality>  | <YYYY-MM-DD> |
| Coverage segment     | <segment>          | Measured     | <surface>| <locality>  | <YYYY-MM-DD> |
| Local pack present   | <yes/no>           | Measured     | <surface>| <locality>  | <YYYY-MM-DD> |
```

Every `Measured` row carries source, market and date. A row without them is `Unknown` with a reason, never a bare number.

### 3.2 The rejected-alternatives table

At least two rows. Each names the term, what it lost on, the value that decided it, and that value's label.

```
| Term      | Why it lost                              | Value that decided it        | Label    |
|-----------|------------------------------------------|------------------------------|----------|
| <term-b>  | SERP-read intent is <class>, not <class> | <the observed SERP finding>  | Measured |
| <term-c>  | Brand-contaminated top ten               | <n> entity results at 1–<n>  | Measured |
| <term-d>  | Already owned by <existing page>         | <the owning page>            | Measured |
```

"It lost on judgement" is not a row. Every row names something that was read.

**Why two rows minimum.** One rejected alternative is a comparison; zero is an assertion. The point of the table is that a later session can see the shape of the field, not just the winner.

---

## 4. Deciding when the evidence is `Unknown`

A decision made on `Unknown` demand is legitimate. A decision that silently treats `Unknown` as zero is not.

| Situation | What the Skill does |
|---|---|
| Demand `Unknown` for **every** candidate | Decide on criteria 1–4. Write into the rationale: `Demand was Unknown for all candidates; selected on <criterion>.` Continue-silently gate 1 |
| Demand `Unknown` for **some** candidates | Do not let the `Unknown` candidates lose on demand — they have no demand value to lose on. If they survive criteria 1–4, they enter the tie in criterion 5 as `Unknown`, and the rationale says the comparison could not be made |
| A tool reported `0` and the pack recorded `Unknown — tool reports 0` | Treat it as `Unknown`, never as low demand. `docs/decisions.md` D14 exists because this was the mechanism by which a real candidate was discarded |
| SERP not observed for a candidate | It cannot be the primary. Criterion 1 cannot be evaluated, and criterion 1 is a gate. Mark it `held` and say which read is missing |
| Every candidate is `Unknown` on criteria 1–5 | Stop. There is no trail to build. Report `stopped` with what would resolve it |

The rationale's last line is always the list of criteria that were `Unknown` for all candidates, or the word `none`. That line is what makes an `Unknown`-heavy decision reviewable rather than merely defensible.

---

## 5. Re-verifying an inherited decision

Run for every page that already exists in the cluster, at `SKILL.md` step 2 — **before** the evidence pack is required, and on every run. This pass is the reason the Skill can be pointed at an existing cluster and say something useful about it, including when no pack exists for that cluster at all.

For each existing page, find four things:

| What | Where to look | If not found |
|---|---|---|
| The primary keyword it declares | The planning record's owned fields; the page's own stated target | `Unknown — no declared primary` |
| The date the metrics behind it were read | The archived research alongside the page; a dated export; a dated snapshot in the record | `Unknown — no snapshot date` |
| The source those metrics came from | The same | `Unknown — no snapshot source` |
| Where its rejected alternatives are recorded | The archived research; the planning record | `Unknown — no rejected alternatives recorded` |

**A page missing the snapshot date or the snapshot source is a defect and is named as one.** Not a gap, not a nice-to-have. Write it into the Re-verification Defects list with the consequence stated plainly:

```
| Page      | What is missing                    | Consequence                                              |
|-----------|------------------------------------|----------------------------------------------------------|
| <page>    | Snapshot date and snapshot source  | The primary-keyword choice cannot be re-verified. Whether it is still correct is Unknown, and re-deciding it would be a new decision, not a check. |
```

The list is written every run, including when it is empty, in which case it reads `none`. A defect list that only appears when there are defects is documentation, not enforcement (`references/skill-contract.md` §4).

### What re-verification does not do

It does not re-run the research. It does not silently re-decide the page's target. It does not mark a page wrong: **a sound architecture with no surviving snapshot is not a bad decision, it is an unreviewable one**, and those are different findings. The correct output is the defect plus what would resolve it — a fresh `seo-geo-research` run on that page's topic, whose pack a later architecture run can then use.

---

## 6. What this file does not decide

The term is a target, not a phrase. Everything below belongs to the Skill named in `authority.authority_override_skill` and is never recommended here:

- Whether the term appears in the heading, and in what words
- How the claim around it is phrased, and how strong that claim is
- Title tag and meta description wording
- CTA framing, urgency, specificity

There is no selection gain that justifies crossing that line (policy kernel §1).
