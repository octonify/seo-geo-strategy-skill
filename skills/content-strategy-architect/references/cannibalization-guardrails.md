# Cannibalization Guardrails

Owned by [`../SKILL.md`](../SKILL.md) steps 4 and 8. The overlap test that decides one page or two, the ownership rule, the conflict checks, and the resolution ladder.

---

## 1. What is being prevented

Two pages on the same site competing for the same query. The cost is not only that one of them loses — it is that neither accumulates the signal the other is splitting, and that nobody can tell which page is supposed to win.

The prevention happens at architecture time, which is why it lives here. Detecting it after publication is a different lifecycle and is outside this bundle (`docs/architecture.md` §6).

---

## 2. The overlap test — one page or two

The question "do these two terms need two pages?" is answered by observation, not by how different the phrases look.

### The rule

For two candidate terms, count how many URLs appear in **both** observed top tens.

| Shared URLs in the two top tens | Verdict | Meaning |
|---|---|---|
| ≥ 4 | **One page** | The engine is returning substantially the same set for both. Two pages would compete |
| ≤ 3 | **Two pages** | The engine distinguishes the queries. Two pages can each own one |
| Either SERP not observed | **`Unknown` — one page for now** | Not splittable on absent evidence. See below |

**The threshold is 4 of the top ten, and the record states it as a sentence every run.** Published practice puts the useful band at roughly 3–6 shared URLs, with 4 the common middle; the figure is a convention, not a measurement, so it is stated openly rather than applied invisibly. An operator who wants a stricter or looser cluster changes the number and the record shows which number was used.

### Why an unobserved pair defaults to one page

The conservative direction is not obvious, so it is fixed here rather than decided ad hoc.

Splitting creates a second page. If the split was wrong, two pages now compete and the damage is live and hard to unwind. Not splitting leaves one page and a held term; if that was wrong, the cost is a page that was not built yet, and building it later costs nothing that was not already going to be spent.

So: **absent evidence never authorises a new page.** The pair is marked `Unknown`, the second term is `held`, and the record names which SERP was missing. Continue-silently gate 3.

### Recording it

```
Overlap threshold: two terms share one page when their observed top tens have
4 or more URLs in common; 3 or fewer means separate pages; an unobserved SERP
on either side means the pair is Unknown and is not split.

| Candidate | Overlap count | SERPs counted            | Verdict  | Label      |
|-----------|---------------|--------------------------|----------|------------|
| <term-b>  | 6             | <term-a>, <term-b>       | member   | Calculated |
| <term-c>  | 1             | <term-a>, <term-c>       | member   | Calculated |
| <term-d>  | —             | <term-d> not observed    | held     | Unknown    |
```

Every count is `Calculated` and names the two reads it counted. A count with no named reads is not evidence.

---

## 3. The ownership rule

**One primary term, one owning page.** Enforced by `Done when` item 11: the Term Ownership table has one row per primary term, and no term appears twice.

```
| Primary term | Owning page | Conflicts found        |
|--------------|-------------|------------------------|
| <term-a>     | <page-1>    | none                   |
| <term-b>     | <page-2>    | <what was found>       |
```

A term owned by two pages is not a finding to note and move past. It is a defect in the map, and the map is changed before the record is emitted.

---

## 4. The three conflict checks

Run against existing pages as well as pages this run proposes. Skipping existing pages is how cannibalization gets built deliberately.

### 4.1 Map-internal conflict

Two pages in this cluster map claim the same owning term.

*Detected by:* the Term Ownership table. *Resolution:* merge them, or re-target one and show the overlap count that justifies keeping both.

### 4.2 Existing-page conflict

A page outside this run already declares or already ranks for the term a proposed page would own.

*Detected by:* the inventory from step 2, plus the pack's own-site coverage rows — a candidate segmented `Held` or `Contested` has an own-site URL already in that SERP.

*Resolution:* stop-and-ask gate 7. The three options are extend the existing page, re-target the new page, or retire the existing one. **Never create the second page silently.**

### 4.3 Boundary conflict

Two pages whose boundary sentences do not name each other, or name each other inconsistently.

*Detected by:* reading the Cluster Map's boundary column as a set. Every member's sentence names at least one sibling, and where two pages name each other the descriptions agree.

*Resolution:* rewrite the boundaries. This is structural scope, not language, and is decided here.

### When own-site coverage was never established

The pack may carry `Unknown` on the own-site axis for every candidate — the case where no crawl, inventory or sitemap was available. Then check 4.2 cannot run.

Record it as `Unknown — own-site coverage not established in the pack`, and mark **every** `create` disposition in the map as provisional on that check. Do not treat unestablished coverage as absent coverage; that turns every row into a false "nothing exists here" and is precisely how a duplicate page gets authorised.

---

## 5. The resolution ladder

When a conflict is real, these are the moves, in the order they are considered:

| # | Move | Use when |
|---|---|---|
| 1 | **Extend the existing page** | The existing page's intent matches and it already has the term's coverage segment. Cheapest, and it consolidates rather than splits |
| 2 | **Re-target the new page** to a term the overlap test shows is separable | The cluster genuinely needs a second page and a distinct term exists with ≤ 3 shared URLs |
| 3 | **Retire the losing page**, routing its inbound links to the owner | Two pages exist, one clearly owns the term, and the other has no distinct term of its own |
| 4 | **Stop and report** | None of the above is decidable from the evidence available |

Move 3 is a recommendation only. Retiring, redirecting, merging or unpublishing a live page is a change to a live object and is never performed here (policy kernel §1). The record names the page, names the owner, and stops.

---

## 6. Reading a query export for conflicts

A first-party query export can show, for one query, which of the site's URLs the engine has been returning. Read once, that answers check 4.2 directly and better than an inventory can.

**The boundary is the operation, not the source** (`docs/decisions.md` D21). Permitted: a single read of which URLs currently serve a query, used as `Measured` evidence at the export date. Forbidden: retaining exports to compare, reading position change, any "was 12, now 8" framing, or a scheduled re-read. A run that finds itself comparing two exports has left this bundle's scope and stops.

Where no export is available, check 4.2 runs from the inventory and the pack's coverage rows, and the record says which source answered it.
