# Run Report — Author `skills/content-strategy-architect/SKILL.md` — 2026-08-02

## Brief

Commit four shared-layer fixes already on disk from the coordinating agent, then apply the D23 follow-up in `seo-geo-research`. Then author the bundle's second Skill, `content-strategy-architect`, conforming to the settled shared layer (`policy-kernel.md`, `skill-contract.md`, `architecture.md`, D1–D23) without restating or revising it. Consume the `seo-geo-research` evidence pack as an input contract. Enforce D8's evidence trail and D9's aggregate cluster demand as checkable items rather than advice. Build the planning-record writer against policy kernel §6, stopping rather than matching rows by title similarity. Cherry-pick from Apache-2.0 source packages 26, 27, 18 and 17 reproducing no text, validate every methodological claim externally before encoding it, and record every non-obvious call as a dated decision. Deliver the Skill, its reference files, decision entries, a `VERSIONS.md` update, this report, and commits.

## Handoff summary

- **Skill:** content-strategy-architect (authoring run)
- **Unit:** One Skill — `skills/content-strategy-architect/`
- **Status:** complete
- **Produced:** `skills/content-strategy-architect/SKILL.md`; eight files under `skills/content-strategy-architect/references/`; `docs/decisions.md` D24–D33; `VERSIONS.md` Unreleased; this report; two preceding fix commits
- **Evidence basis:** 7 Measured (six external searches run and read, plus one direct read of Google's structured-data feature gallery), 9 User-provided (settled foundation files, the four source packages, the validation-case artifacts), 2 Calculated (the planning-record row and cluster counts derived from the validation case's CSV), 0 Estimated, 2 Unknown (listed under *Open for the coordinating agent*)
- **Assumptions:** Skill frontmatter carries `version: 0.0.0-unreleased` (D19). The D10 validation config was assembled from observable project facts because the consuming project has no installed `project-config.yaml` for this bundle. The validation record was written to scratchpad rather than committed — it is a test artifact, not a bundle deliverable. Entries are dated 2026-08-02, which is the date reported by the environment and by every commit timestamp in this repository; see *Open for the coordinating agent* item 2.
- **Open questions:** Two, in the section of that name.
- **Recommended next:** return to operator

## Delivered

| File | New/Modified | What it contains |
|---|---|---|
| `references/skill-contract.md` | Modified | §5 evidence-basis line now enumerates all five labels (coordinating agent's edit, committed here) |
| `project-config.schema.yaml` | Modified | Optional `research_output.path` (coordinating agent's edit, committed here) |
| `skills/seo-geo-research/references/intent-classification.md` | Modified | Worked example de-identified (coordinating agent's edit, committed here) |
| `skills/seo-geo-research/SKILL.md` | Modified | D23 follow-up: `Calculated` counted directly; folding convention removed |
| `skills/seo-geo-research/references/evidence-pack-template.md` | Modified | Same, in the handoff block |
| `skills/seo-geo-research/references/metric-label-map.md` | Modified | Same, in §§2 and 4 |
| `skills/content-strategy-architect/SKILL.md` | New | Frontmatter with a three-way negative boundary; the six required sections in contract order; sixteen mechanically-checkable `Done when` items; eleven stop-and-ask gates with numbered options and ten continue-silently gates with stated defaults; fourteen procedure steps each naming its output and its permitted evidence labels |
| `references/primary-keyword-selection.md` | New | Six selection criteria in applied order; the mandatory D8 trail (dated snapshot plus a two-row-minimum rejected-alternatives table); the rule for deciding under `Unknown`; the re-verification pass on inherited decisions |
| `references/cluster-architecture.md` | New | Roles and dispositions; the boundary-sentence rule; member-count guidance treated as guidance; aggregate cluster demand as a floor, flagged as a D9 addition |
| `references/cannibalization-guardrails.md` | New | The SERP-overlap test with its stated threshold; the one-term-one-page ownership rule; three conflict checks including against existing pages; the resolution ladder; the query-export boundary per D21 |
| `references/internal-link-map.md` | New | Required cluster wiring; row shape carrying a target concept and never an anchor phrase; evidenced cross-links only; the wording boundary stated as a table |
| `references/schema-decision.md` | New | The two-question separation; the dated documentation read; type selection; the visible-content constraint; answer-engine structure split into supported, contested, and not-encoded |
| `references/content-brief-template.md` | New | The full brief, filled literally, with an eight-row exclusion check and a named list of everything the voice Skill owns |
| `references/planning-record-protocol.md` | New | Three preconditions; the identification sequence with no title fallback; intent-versus-state field classification; two write points; the stamped Record Writes table; the overwrite gate |
| `references/cluster-record-template.md` | New | The full output record, filled literally |
| `skills/content-strategy-architect/.gitkeep` | Deleted | Placeholder, superseded |
| `docs/decisions.md` | Modified | D24–D33 appended. D1–D23 untouched |
| `VERSIONS.md` | Modified | Unreleased section updated with the shared-layer fixes, what was added, the four flagged methodology changes, and the validation result |
| `docs/run-reports/2026-08-02-content-strategy-architect.md` | New | This file |

## Decisions recorded

| ID | Decision | Accept/Reject | Basis |
|---|---|---|---|
| D24 | Architecture decides link targets, never anchor wording | Reject the source's suggested-anchor column and its anchor-share thresholds | Policy kernel §1 gives wording to the voice Skill; the thresholds are unsourced percentages about wording, failing §2 as well |
| D25 | Reject the structure score, the architecture score, and the anchor score | Reject | D12's reasoning transfers unchanged. These are worse in one respect: the penalty weights are stated to the point with no source |
| D26 | Schema decisions separate documented rich-result eligibility from entity value; `FAQPage` and `Service` are both `no` | Accept the mapping question, correct the answers | Addition — flagged. Direct read of Google's feature gallery plus external search. The source maps a service page to a "Service snippet" that does not exist |
| D27 | Aggregate cluster demand is a floor, never a total | Addition — flagged | D9 as written does not survive a partial pack; summing requires giving `Unknown` a number, which is the failure policy kernel §2 names |
| D28 | Observed SERP overlap decides one page or two; unobserved pairs are never split | Addition — flagged | Externally validated band of 3–6 shared URLs, 4 the common middle. The unobserved default is fixed because absent evidence must never authorise a new page |
| D29 | Re-verification runs before the evidence pack is required | Decision, from the validation run | The draft required the pack at step 2 and would have failed its own D10 case on sequencing while every rule needed to pass was already correct |
| D30 | Planning record gets a write rule per owned stage; state fields are not written | Addition — flagged | The documented failure was a write rule for the last stage only. State fields inside `owned_fields` reproduce it in miniature — D2's lesson at column scale |
| D31 | Reject package 17 in full | Reject | Language, invented CTR metrics, and post-publication A/B measurement. Three independent grounds |
| D32 | Source package cherry-pick ledger, packages 17, 18, 26, 27 | 17-row accept/reject ledger | Every candidate file read before its verdict. No text reproduced |
| D33 | Proposal: optional `architecture_output.path` | Proposal recorded, not implemented | Schema is shared layer. `research_output.path` deliberately not reused — silently widening a key's meaning is worse than leaving the question open |

## External validation

Every methodological claim encoded was checked before being written, not after. All reads on 2026-08-02.

| Claim encoded | Source consulted | Outcome |
|---|---|---|
| `FAQPage` no longer produces a rich result for any site, including the government and health verticals that retained eligibility after the 2023 restriction | Search: FAQ rich result deprecation status and remaining eligibility | **Confirmed** — deprecation notice dated 2026-05-07, with Search Console and Rich Results Test support removed in phases thereafter. Supports D26 |
| `Service` is not a documented Google rich-result feature, and `LocalBusiness` is | Direct read of Google's structured-data feature gallery | **Confirmed** — 30 documented features; `Service` absent, `Local business` present, `FAQ` absent. This is the evidence that makes the source's "Service snippet" row wrong rather than merely dated. Supports D26 |
| Cannibalization is detected by asking which of a site's URLs serve one query, read once — not by comparing positions over time | Search: cannibalization detection using Search Console query-to-pages | **Confirmed**, and it sits cleanly inside D21's boundary: the permitted operation is a one-time read, not a period comparison. Supports `cannibalization-guardrails.md` §6 |
| Two terms belong on one page when their SERPs overlap substantially; the useful threshold band is roughly 3–6 shared URLs of the top ten, with 4 common | Search: SERP overlap thresholds for keyword grouping | **Confirmed**, with the boundary that the figure is a convention rather than a measurement — which is why D28 requires the record to state which number was used |
| Pillar-and-cluster architecture with bidirectional pillar↔member linking is current practice, and fewer deeper clusters outperform more thinner ones | Search: topic cluster and pillar page architecture, 2026 | **Confirmed** for the structural claims. The accompanying traffic-gain and article-count figures were **not** encoded — they vary widely between sources and carry no reproducible basis, so `cluster-architecture.md` §2 treats the count as guidance and states so |
| One primary keyword per page, and intent match ahead of search volume when selecting it | Search: primary keyword selection method, intent versus volume | **Confirmed** — current guidance is explicit that volume-first selection is outdated and that a term whose SERP answers a different question cannot be won at any volume. Supports the criterion ordering in `primary-keyword-selection.md` §2 |
| An effective brief enumerates non-negotiables without dictating sentence-level choices | Search: SEO content brief composition | **Confirmed**, and it independently states this bundle's own voice boundary. With one divergence: published brief templates routinely include tone, brand voice, and word count. Those are **excluded** here, because policy kernel §1 assigns them to the client's voice Skill — recorded in `content-brief-template.md` §2 rather than silently dropped |
| For answer-engine citation, the clearest answer near the top of the page, heading hierarchy reflecting real structure, and self-contained sections are supported; deliberate fragmentation for machine extraction is contested | Search: GEO and AI Overview citation, content structure | **Confirmed as split.** Google's guidance says writing for humans is sufficient; independent GEO research reports gains from granular structuring. Encoded as a recorded disagreement rather than resolved, following D15's pattern. Citation-rate percentages found alongside were not encoded |

## Drift control

- **Scope-expansion proposals recorded but NOT implemented:** one. An optional `project-config.schema.yaml` key `architecture_output.path`, so the operator is not asked for an output directory at run time (D33). Not implemented — the schema is shared-layer foundation, and the existing `research_output.path` was deliberately not repurposed. Nothing else: content calendars, editorial workflow, publishing cadence, performance measurement, whole-site information architecture, URL taxonomy, navigation design, orphan sweeps, redirects, JSON-LD generation, schema validation workflows, and CTR A/B testing were all encountered across packages 17, 18, 26 and 27 and all rejected rather than carried in as essential. See the D32 ledger.
- **Shared-layer problems recorded but NOT edited:** none. The four authorised edits were reviewed and committed as `5700726`; the D23 follow-up inside `seo-geo-research` was committed as `51dd734`. `references/policy-kernel.md`, `references/skill-contract.md`, `docs/architecture.md` and `project-config.schema.yaml` were re-read in full afterwards and no further problem was found in any of them. No shared-layer file was modified beyond the authorised set.
- **Settled decisions whose "reverses if" condition may be met:** none. Three were checked specifically. D12's condition — architecture proving unable to decide without a pre-computed rank — did **not** fire: the six ordered criteria in `primary-keyword-selection.md` decide without any score, including when demand is `Unknown` for every candidate. D1's condition did not fire either; the reference material was read closely and proved materially *wrong* on schema eligibility, not better. D21's condition — a consuming project acquiring a rank-tracking capability — is unchanged.
- **Contract rules re-checked before commit:** `skill-contract.md` §2 confirmed: frontmatter complete, with a negative boundary naming all three neighbours — `seo-geo-research`, the voice Skill, and `local-presence-manager`. §3 confirmed: all six required sections present, in order (Skill Contract → Data sources → Decision gates → Procedure → Output → Handoff summary). §4 confirmed: all sixteen `Done when` items are checkable by looking at the record, and item 16 makes the check fire unconditionally by requiring the check table to be written every run. §6 confirmed by scan: no client name, service, city, domain, tool, plugin, or project path appears in any of the nine authored files; every project value is read from a named config key. §7 confirmed: long tables, taxonomies, and templates live in `references/`, and `SKILL.md` reads end to end.

## Validation test

**D10 case: Hormone Health cluster. Result: pass.** Full run recorded in the session scratchpad as `d10-hormone-health-validation.md`.

**Method.** The drafted Skill was executed against the consuming project's planning database and its archived hormone content map. The known answer was not consulted while running.

**The two gates that fired first, correctly.** The named unit, "Hormone Health", resolves in the planning record's own cluster column to **seven** clusters plus a service page and a lead magnet — so gate 4 fired, and the run proceeded per its option 2. No `seo-geo-research` pack exists for any hormone cluster, so gate 3 fired and the run proceeded as a re-verification-only run.

**The finding, reached without being told to look for it.** Across all 35 rows: 33 declare a primary focus keyword, and **zero** carry a snapshot date, a snapshot source, or a record of rejected alternatives. Every one of the 35 was written into the Re-verification Defects list with the consequence stated — the choice cannot be re-verified, and re-deciding it would be a new decision rather than a check.

**The absence was searched for before being declared.** The planning record has no column for volume, difficulty, observation date, or source — confirmed by scanning all 35 headers. No research directory exists for any hormone topic, though the sibling service has one. The archived hormone content map was opened and read in full: eleven sheets, 644 populated cells, and not one volume figure, difficulty figure, observation date, or rejected-alternatives table. Its only references to a metric source are three narrative lines, two of which instruct that validation *should* be done before writing. The instruction survived; the validation did not.

**The Skill separated the two findings, which is the part that matters.** The architecture is sound and the record says so: all 35 rows carry a cluster, a content role, an explicit boundary sentence, and an internal link target, and the Skill's own boundary and term-ownership requirements are already satisfied. The defect is evidentiary, not architectural. A sound architecture with no surviving snapshot is not a bad decision — it is an unreviewable one, and `primary-keyword-selection.md` §5 requires those to be reported as different things.

**Four further findings the run produced unprompted.** Five rows declare `FAQPage`, which per the 2026-08-02 documentation read is entity-value only and earns no rich result. Eleven rows declare `MedicalWebPage` and one `MedicalBusiness`; neither appears under those names in the documented feature gallery, recorded as a check rather than a correction. The planning record mixes field kinds exactly as `planning-record-protocol.md` §4 predicts — one status cell holds a 400-character narrative including an unresolved post-publication issue, a state column being used as a log because no field owns that stage. And `row_identifier_field` is undeclared in the consuming project, which would fire the blocking gate before any write.

**The fault the validation caught.** In the first draft, the no-pack gate fired at step 2, ending the run before the re-verification pass could execute. The Skill would have failed this case on sequencing alone while every rule it needed in order to pass was already written correctly. The inventory and re-verification pass now run at step 2 ahead of pack ingestion, gate 3 gained a re-verification-only option, and `Done when` item 16 was widened to admit `n/a` for items 5–14 on such a run. Recorded as D29.

## Open for the coordinating agent

1. **`architecture_output.path` needs a decision, and it is a shared-layer edit.** Same shape as the `research_output.path` question the coordinating agent settled in D22. Without it the operator is asked for an output directory at run time, or the record is emitted in session only. Neither is broken. `research_output.path` was deliberately not reused, because a cluster architecture record is not research output and quietly widening the key's meaning would be worse than the open question. D33 records the proposal and does not implement it.

2. **Repository dates are inconsistent by one day, and this report did not propagate the error.** `docs/decisions.md` D11–D23 and the previous run report are dated 2026-08-03. Every commit timestamp for that work reads 2026-08-02, as does the environment's own date for this session. This run's entries are therefore dated 2026-08-02, which makes D24 appear to precede D23 by date while following it in sequence. Past reports are never edited and settled decision entries were not touched, so the discrepancy is reported rather than corrected. If the coordinating agent prefers monotonic dates, correcting D11–D23 is a one-line-per-entry change it can authorise; this run did not assume that authority.

## Commit

`fed5a53` — `feat: author content-strategy-architect skill and its reference layer`

Preceded in this session by two fix commits carrying the authorised shared-layer work:

- `5700726` — `fix: resolve shared-layer gaps raised by the seo-geo-research run`
- `51dd734` — `fix: count Calculated directly in seo-geo-research, per D23`

The feature commit carries every deliverable: the Skill, its eight reference files, D24–D33, the `VERSIONS.md` update, and this report. Not tagged.

A report cannot contain its own commit hash — writing the hash in changes the tree and so changes the hash. This line therefore names the commit containing the deliverables, and is corrected by a one-line follow-up commit that contains nothing else.
