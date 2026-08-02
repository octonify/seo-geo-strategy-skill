# Run Report — Author `skills/seo-geo-research/SKILL.md` — 2026-08-03

## Brief

Author the first of the bundle's three Skills, `seo-geo-research`, conforming to the settled shared layer (`policy-kernel.md`, `skill-contract.md`, `architecture.md`, D1–D10) without restating or revising it. Cherry-pick from Apache-2.0 source packages 06–11 reproducing no text, validate every methodological claim externally rather than relying on precedent or on the source bundle, encode the better method where past practice was weak and flag it as an addition, and record every non-obvious call as a dated decision. Deliver the Skill, its reference files, decision entries, a `VERSIONS.md` update, this report, and one commit.

## Handoff summary

- **Skill:** seo-geo-research (authoring run)
- **Unit:** One Skill — `skills/seo-geo-research/`
- **Status:** complete
- **Produced:** `skills/seo-geo-research/SKILL.md`; six files under `skills/seo-geo-research/references/`; `docs/decisions.md` D11–D20; `VERSIONS.md` Unreleased; this report
- **Evidence basis:** 8 Measured (external searches run and read), 6 User-provided (settled foundation files, source packages, validation artifacts), 0 Estimated, 3 Unknown (listed under *Open for the coordinating agent*)
- **Assumptions:** Skill frontmatter carries `version: 0.0.0-unreleased` because no tag exists (D19). The D10 validation config was assembled from known project facts because DNC has no installed `project-config.yaml` for this bundle. The validation pack was written to scratchpad rather than committed — it is a test artifact, not a bundle deliverable.
- **Open questions:** Three, in the section of that name.
- **Recommended next:** return to operator

## Delivered

| File | New/Modified | What it contains |
|---|---|---|
| `skills/seo-geo-research/SKILL.md` | New | Frontmatter with negative boundary naming `content-strategy-architect`; the six required sections in contract order; twelve mechanically-checkable `Done when` items; seven stop-and-ask gates with numbered options and eight continue-silently gates with stated defaults; twelve procedure steps each naming its output and its permitted evidence labels |
| `skills/seo-geo-research/references/keyword-universe-sources.md` | New | Eight discovery sources with the label each may carry; procedures for all three `access_mode` values; the zero-tool path; modifier patterns rewritten around provider-and-place forms |
| `skills/seo-geo-research/references/intent-classification.md` | New | Four-class matrix, seven-value sub-intent layer marked as an addition, the dual-pass procedure, and the disagreement rule |
| `skills/seo-geo-research/references/serp-read-protocol.md` | New | The observation rule; per-read capture fields; seven-type result taxonomy; ten-feature checklist; six named findings checks; observed difficulty as separately-labelled inputs with no composite |
| `skills/seo-geo-research/references/metric-label-map.md` | New | Per-metric permitted and forbidden labels; the four rules generating them; the zero-volume rule and the population-ratio derivation; the evidence-basis counting convention |
| `skills/seo-geo-research/references/competitor-and-gap-mapping.md` | New | Competitor set derived from SERP appearances; profile fields; five-way coverage segmentation; gap rows bound to an evidencing URL; format and question passes |
| `skills/seo-geo-research/references/evidence-pack-template.md` | New | The full output template, filled literally |
| `skills/seo-geo-research/.gitkeep` | Deleted | Placeholder, superseded |
| `docs/decisions.md` | Modified | D11–D20 appended. D1–D10 untouched |
| `VERSIONS.md` | Modified | Unreleased section updated with what was added, the three flagged methodology changes, and the validation result |
| `docs/run-reports/2026-08-03-seo-geo-research.md` | New | This file |

## Decisions recorded

| ID | Decision | Accept/Reject | Basis |
|---|---|---|---|
| D11 | Research produces evidence and names no target | Reject source delivery sections and the `Opportunity` formula | `architecture.md` §2 boundary; a Skill doing both phases has neither completion criterion |
| D12 | Reject every composite priority score (four models) | Reject | A composite from mixed `Measured`/`Estimated`/`Unknown` inputs carries no honest label, and requires `Unknown` to become a number — the failure policy kernel §2 names. Ranking is architecture's decision |
| D13 | SERP composition is `Measured` or `Unknown`, never `Estimated` | Addition — flagged | Difficulty is built on composition; an inferred composition becomes an invisible inferred difficulty. Externally validated |
| D14 | A tool-reported zero volume is `Unknown`, never a demand figure | Addition — flagged | Validation case shows 66 of 204 archived rows carrying blank or `0` volume, one of them rejected for "insufficient demand" on a data-coverage artifact. Externally validated |
| D15 | Intent classified twice; SERP wins; sub-intent layer added | Accept taxonomy rewritten; addition flagged | `skill-contract.md` §4 corollary — state which record wins. Validation case shows the same string reading Informational nationally and Navigational locally. Externally validated |
| D16 | Search Console query mining is a discovery source, not rank tracking | Boundary interpretation | Distinguishes one-time demand discovery from position monitoring, which `architecture.md` §6 excludes. Flagged below for confirmation |
| D17 | Research reads and writes no planning record | Reject | Policy kernel §6 needs an unambiguous target row; no page exists until architecture decides one should. Recreating D2's mixed-lifecycle failure otherwise |
| D18 | No config key for research output path; operator supplies it | Proposal recorded, not implemented | Schema is shared-layer foundation this task may not edit |
| D19 | Skill files carry `version: 0.0.0-unreleased` until the first tag | Decision | `skill-contract.md` §2 requires a version; no tag exists; a false version breaks the byte-identical-to-tag rule |
| D20 | Source package cherry-pick ledger, packages 06–11 | 22-row accept/reject ledger | Every candidate file read before its verdict. No text reproduced |

## External validation

Every methodological claim encoded was checked by search on 2026-08-02/03 before being written, not after.

| Claim encoded | Source consulted | Outcome |
|---|---|---|
| Tool difficulty scores are estimates that vary substantially between tools; manual SERP inspection is required to catch what a score misses | Search: keyword difficulty tool reliability and manual SERP verification, 2026 | **Confirmed** — supports D13 and the refusal in D12 to build another composite |
| The live SERP is the ground-truth authority for intent classification | Search: search-intent classification and SERP verification method, 2026 | **Confirmed** — supports D15 Pass B and the disagreement rule |
| Four-class intent is no longer granular enough; narrower sub-intents each imply a different format, and SERP-feature presence is the most reliable secondary signal | Search: same | **Confirmed** — supports the sub-intent layer, flagged as an addition |
| A tool reporting zero volume for a small or geo-modified market is reporting missing coverage, not absent demand; the population-ratio derivation is the common workaround and is itself an estimate | Search: local keyword research, low local volume, national cross-check, 2026 | **Confirmed** — supports D14, including admitting the derivation only as a labelled `Calculated` value beside the `Unknown` rather than instead of it |
| AI Overviews now trigger on a large and growing share of queries, concentrated on informational and question-format ones; citation correlates with position and with structural clarity | Search: generative engine optimization, AI Overview citation triggers, 2026 | **Confirmed** — supports making the GEO surface read step 10 rather than an optional extra |
| A keyword universe is assembled from multiple discovery sources before filtering; autocomplete, PAA and related searches are viable free sources yielding tens of variants per seed | Search: keyword universe construction, PAA and autocomplete free methods | **Confirmed** — supports the eight-source model and the claim that the zero-tool path is a complete run rather than a degraded one |
| Tool search volumes are approximations whose methodology differs per platform and whose values move over time | Search: search volume snapshot, reproducibility of keyword metrics | **Confirmed**, with a boundary. It validates the requirement that every `Measured` value carry its tool, market and date. It does **not** change policy kernel §2's definition of `Measured` as "read directly from a tool", and the kernel was not reinterpreted |
| Local pack presence is a near-fixed feature of local service SERPs and the strongest single signal that the engine reads a query as provider-seeking | Search: local pack as SERP signal for local intent, 2026 | **Confirmed** — supports the intent Pass B ordering and the local-pack-dominance finding |
| Search engines favour recognised brand entities, and a brand whose name is a generic term distorts the results for that term | Search: branded entity dominance and generic-term contamination | **Confirmed** — supports the brand-contamination finding, which the validation case then independently exercised twice |

## Drift control

- **Scope-expansion proposals recorded but NOT implemented:** two.
  1. An optional `project-config.schema.yaml` key `research_output.path`, so the operator is not asked for an output directory at run time. Recorded in D18. Not implemented — the schema is shared-layer foundation.
  2. Nothing else. Technical SEO, Core Web Vitals, backlink profiling, rank tracking, site-stage fit, content calendars and priority tiers were all encountered in packages 06–11 and all rejected rather than carried in as "essential"; see the D20 ledger.
- **Shared-layer problems recorded but NOT edited:** one. `project-config.schema.yaml` defines no key for a research output directory, which is why D18 exists. `references/skill-contract.md`, `references/policy-kernel.md` and `docs/architecture.md` were read in full and no problem was found in any of them. No shared-layer file was modified.
- **Settled decisions whose "reverses if" condition may be met:** none. D1's condition in particular did not fire — the reference system's methodology was read closely, its research/decision phase split was adopted (already settled), and its four scoring models were rejected on grounds recorded in D12; nothing in it proved materially better on the validation case.
- **Contract rules re-checked before commit:** `skill-contract.md` §3 re-read and every required section confirmed present in order (Skill Contract → Data sources → Decision gates → Procedure → Output → Handoff summary). §2 frontmatter confirmed complete including the negative boundary. §4 confirmed: all twelve `Done when` items are checkable by looking at the pack, and item 12 makes the check itself fire unconditionally by requiring the check table to be written every run. §6 confirmed: no client name, domain, service, city, tool or project path appears in any authored file; every project value is read from a named config key. §7 confirmed: long tables and templates live in `references/`.

## Validation test

**D10 case: Gut Health keyword research. Result: pass, with one declared limitation.**

Method. The drafted Skill was executed against only the seven raw Semrush artifacts in `…/service-gut-health/content-item/research/`. The archived `README.md`, both CSVs, and the service-page handoff document were **not opened until the pack was written**. The pack is at `…/scratchpad/d10-gut-health-validation-pack.md`.

**Candidate set.** The archive's local Kirkland validation table holds six terms. The pack independently produced a SERP read for all six, plus `gut health doctor`, which the archive screenshotted but omitted from its local table — a superset of 7 against 6.

**Metrics.** Every overlapping value matches exactly. National: `gut health doctor` 880/32, `gut health doctor near me` 590/28, `gut health specialist` 480/21, `gut health clinic` 140/23, `functional medicine gut health` 140/13, `functional medicine for gut health` 110/8. Local: 10/24, 10/14, 10/38, 0→`Unknown`/12, 0→`Unknown`/5, 0→`Unknown`/17.

**Findings reproduced without being shown them.** The archive rejects `gut doctor` as primary "because SERP is mixed and brand-influenced". The pack fired its brand-contamination check on that term independently, naming the three entity results that cause it (`theguthealthdoctor.com` at 1, `theguthealthmd.com` at 8, an Apple podcast titled *The Gut Doctor* at 3) and counting exactly one comparable local provider in the top nine. The archive records `naturopathic doctor for gut health` as a "strong provider match"; the pack independently found it to be the only provider-seeking term of the seven with no brand entity anywhere in its top nine.

**Findings the archive did not record.** Three. `gut health doctor` and `gut health specialist` both read as Navigational from the SERP despite an Informational tool label, because a brand entity occupies position one — the archive carries only the tool label. `functional medicine gut health` is the sole term of the seven with an AI Overview and the sole term with no local pack, and its top nine contains no comparable local provider at all — a GEO and intent signal the archive does not note. And 66 of the archive's 204 keyword rows carry a blank or `0` volume, including the one term rejected for "insufficient demand" on that basis.

**Where the pack diverges, and why that is the improvement.** The archive treats `naturopathic doctor for gut health` volume `0` as insufficient demand. The pack records `Unknown — tool reports 0` on both axes and states that a populated, locality-set SERP carrying a local pack is evidence the query is *served*, not evidence it is *searched*. This is D14 doing the work it was written for.

**Target.** The archive's primary is `gut health clinic in Kirkland WA`. The pack names no target, by design (D11), and it is correct that it does not. The evidence required to reach that choice is present in it: `gut health clinic` is one of only three head terms with any non-zero local volume, its SERP-read intent is Commercial · Provider-seeking, its local pack is present, and its top nine holds three comparable local providers all carrying zero measurable authority.

**The declared limitation.** The pack's universe is 53 observed terms; the archive's export is 204. The cause is input coverage, not method — the seven screenshots show each tool panel's *total* (299, 1.2K, 951, 1.7K and so on) but only its top five rows. The pack states this in a "Universe coverage caveat" and lists it in its Unknowns table rather than presenting 53 as complete. Two terms in the archive's national table, `gut health` (33,100/65) and `digestive health` (5,400/60), are consequently absent from the pack. Run against the full CSV export rather than seven screenshots, the universe would not have been narrower.

**Incidental finding about the archived case itself.** `gut doctor` has a Kirkland validation screenshot and appears in the service-page handoff's local decision table, but is absent from `DNC-gut-health-keyword-list-2026-07-15.csv` entirely. The archive's screenshot set and its keyword export disagree. Reported, not acted on.

## Open for the coordinating agent

1. **D16 is a boundary interpretation, not a scope expansion — please confirm it.** `architecture.md` §6 excludes rank tracking and performance monitoring. A Search Console query export contains positions. D16 draws the line at *one-time demand discovery* versus *position monitoring over time*, and admits the former as discovery source 2 because first-party impression data is the only `Measured` demand available to a project with no paid tool. If the coordinating agent reads §6 as excluding the export entirely, source 2 is removed and the zero-tool path loses its only measured demand signal.

2. **The `research_output.path` proposal needs a decision, and it is a shared-layer edit.** Without it the operator is asked for an output directory at run time, or the pack is emitted in session only. Neither is broken; both are slightly worse than a config key. D18 records the proposal and does not implement it.

3. **The `Calculated` label has no slot in the `skill-contract.md` §5 handoff block.** The block enumerates Measured / User-provided / Estimated / Unknown; the policy kernel defines five labels. This Skill resolves it by counting `Calculated` values under the weakest label among their inputs and stating that convention in the pack. That is a local resolution to a shared-layer asymmetry, and it will recur in both remaining Skills. Worth settling once, centrally, rather than three times.

## Commit

`a5271e8` — `feat: author seo-geo-research skill and its reference layer`

Single commit, amended once to carry its own hash — a run report that cannot name the commit containing it is not usable by the coordinating agent. Not tagged.
