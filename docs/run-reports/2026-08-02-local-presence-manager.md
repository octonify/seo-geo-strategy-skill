# Run Report — Author `skills/local-presence-manager/SKILL.md` — 2026-08-02

## Brief

Commit two shared-layer edits already on disk from the coordinating agent — the D11–D23 date correction and the optional `architecture_output.path` — then author the bundle's third and last Skill, `local-presence-manager`, conforming to the settled shared layer (`policy-kernel.md`, `skill-contract.md`, `architecture.md`, D1–D35) without restating or revising it. Unit: one business location. In scope: the canonical NAP record, Google Business Profile optimisation, citation priority and per-source status, and location and service-area page plans. Cherry-pick from Apache-2.0 source package 28 — and only its `page-play-builder/references/local.md`, the entity registry being rejected in full by D4 — reproducing no text. Validate every methodological claim externally before encoding it. Get two things right: the NAP record is one exact string per field agreed once, with disagreement a stop-and-ask gate rather than a silent pick; and every listing observation carries a label and a date, with an unchecked directory `Unknown` and never `missing`. Deliver the Skill, its reference files, decision entries, a `VERSIONS.md` update, this report, and one commit. Do not tag.

## Handoff summary

- **Skill:** local-presence-manager (authoring run)
- **Unit:** One Skill — `skills/local-presence-manager/`
- **Status:** complete
- **Produced:** `skills/local-presence-manager/SKILL.md`; six files under `skills/local-presence-manager/references/`; `docs/decisions.md` D36–D45; `VERSIONS.md` Unreleased; this report; one preceding fix commit
- **Evidence basis:** 8 Measured (six external searches run and read, one direct read of the platform's own business-representation guidelines, one live read of the validation case's site), 7 User-provided (settled foundation files, source package 28, the consuming project's own records), 3 Calculated (the NAP comparisons and store counts derived from the validation case), 0 Estimated, 2 Unknown (listed under *Open for the coordinating agent*)
- **Assumptions:** Skill frontmatter carries `version: 0.0.0-unreleased` (D19). The D10 validation config was assembled from observable project facts because the consuming project has no installed `project-config.yaml` for this bundle — which is itself what exercised the observation-only path and exposed the D42 fault. The validation run was kept in session rather than committed; it is a test artifact, not a bundle deliverable. All entries are dated 2026-08-02, the environment date, per D34's standing rule.
- **Open questions:** Two, in the section of that name.
- **Recommended next:** return to operator

## Delivered

| File | New/Modified | What it contains |
|---|---|---|
| `docs/decisions.md` | Modified | D11–D23 heading and in-body dates corrected to 2026-08-02; D34 and D35 appended (coordinating agent's edit, committed here) |
| `project-config.schema.yaml` | Modified | Optional `architecture_output.path` (coordinating agent's edit, committed here) |
| `skills/local-presence-manager/SKILL.md` | New | Frontmatter with a three-way negative boundary; the six required sections in contract order; sixteen mechanically-checkable `Done when` items; ten stop-and-ask gates with numbered options and thirteen continue-silently gates with stated defaults; ten procedure steps each naming its output and its permitted evidence labels |
| `references/observation-label-map.md` | New | Per-observation permitted and forbidden labels; the source list in observation order; the four rules generating the map; the evidence-basis count; and what this record deliberately is not — the D4 rejection stated inside the Skill |
| `references/canonical-nap-record.md` | New | One exact string per field; the eight format choices that have to be decided and who decides them; the three permitted origins and the fourth that does not exist; the character-for-character comparison with its comparison-base rule; the three difference classes; the name field's extra constraint; and site-versus-profile as a finding either way |
| `references/gbp-checklist.md` | New | The dated guideline read; thirteen items each with a stated condition per status value; the presence-not-wording and suitability boundaries; seven things deliberately not checked, each with its reason; and what a completed checklist is and is not worth |
| `references/citation-sources.md` | New | The four-value status vocabulary and why the last two are distinct; the tier list with operator-filled placeholders at tier 5; priority as a reading order rather than a schedule; the three-search zero-tool procedure; the three counts; and unstructured mentions recorded but never pursued |
| `references/location-page-plan.md` | New | The pattern per `service_area_mode`; one locality per page; the element-by-element split of what is decided here and what is not; four dispositions; the duplication constraint with every attached threshold stripped; and page count left unsequenced |
| `references/local-presence-record-template.md` | New | The full record, filled literally, with the sixteen-row Done-when table and six filling rules |
| `docs/decisions.md` | Modified | D36–D45 appended. D1–D35 untouched beyond the authorised commit above |
| `VERSIONS.md` | Modified | Unreleased section updated: all three Skills present, what was added, the four flagged methodology changes, the validation result, and the tagging position |
| `docs/run-reports/2026-08-02-local-presence-manager.md` | New | This file |

## Decisions recorded

| ID | Decision | Accept/Reject | Basis |
|---|---|---|---|
| D36 | Source package cherry-pick ledger, package 28 | 14-row accept/reject ledger | Every candidate file read before its verdict. No text reproduced. Includes a positive re-confirmation of the D4 entity-registry rejection |
| D37 | The website is a NAP source, and every place it states a NAP is its own row | Addition — flagged | The source material never reads the site. Two first-party surfaces disagreeing is the highest-value variance there is, and a one-row-per-site model hides it |
| D38 | Unchecked is `Unknown`, never `missing`; no observation is ever `Estimated` | Addition — flagged | Policy kernel §2 applied to the two mechanisms by which a default was going to creep in. The `Estimated` half is stricter than the kernel, as D13 was |
| D39 | Presence is checked, wording is not — including the profile description | Reject the source's keyword-position instruction | Policy kernel §1 gives wording to the voice Skill, and the threshold is unsourced. External validation shows the description is not a direct ranking input |
| D40 | Reject every unsourced local threshold; keep the direction | Reject, six figures | D31's reasoning transfers unchanged. Quoting somebody else's invented metric is inventing one with an extra step |
| D41 | Local presence plans pages, decides no target, writes no planning row | Decision | `architecture.md` §2 gives page ownership to architecture; D17's planning-row reasoning transfers unchanged |
| D42 | The variance comparison runs without a canonical, against a named base | Addition — flagged, from the validation run | The draft hung the whole comparison off the canonical and would have failed its own D10 case. D29's fault in a second Skill |
| D43 | A dated observation from an earlier session is carried with its date | Addition — flagged, from the validation run | Both alternatives are wrong: presenting stale data as current asserts an unchecked fact; discarding it leaves the comparison unmade |
| D44 | Reviews are not checked here, and the gap is recorded rather than filled | Proposal recorded, not implemented | Externally validated as the second-heaviest local signal, so it is a real gap. Adding it needs `architecture.md` §5 approval, and a separate unit rather than a field |
| D45 | Proposals: `local_presence.service_areas`, and an output-path key for this Skill | Proposals recorded, not implemented | The schema is shared layer. Neither existing path key is reused, per the D33/D35 reasoning |

## External validation

Every methodological claim encoded was checked before being written, not after. All reads on 2026-08-02.

| Claim encoded | Source consulted | Outcome |
|---|---|---|
| Google Business Profile signals carry roughly a third of local pack ranking weight, making them the strongest single local factor | Search: local pack ranking factors 2026, share of weight | **Confirmed** — around 32%, up to roughly 36% in one source, against on-page 19%, reviews 16%, links 15%, behavioural 8%, citations 7%. This is D3's premise and it holds. Carried as third-party context in `gbp-checklist.md` §5 and explicitly not as arithmetic against an individual profile |
| The primary category is the single most influential profile field for local pack placement | Search: same | **Confirmed** — which is why checklist item 6 records the exact string rather than a summary, and equally why the Skill does not guess a better one |
| Inconsistent NAP strings split entity resolution across a business's listings, and duplicate listings are common and damaging | Search: NAP consistency, duplicate listings, entity resolution 2026 | **Confirmed** for the mechanism. The figures found alongside it — a share of consumers losing trust, a citation-count comparison — were **not** encoded; see D40 |
| A profile description is not a direct ranking input; it contributes to completeness and to answer-engine summaries | Search: GBP description as a ranking factor 2026 | **Confirmed**, and it undercuts the source material's keyword-position instruction on its own terms as well as on the wording boundary. Supports D39 |
| The platform's own rules on the name field, P.O. boxes, address precision and signage, service-area address hiding, categories, and hours | Direct read of the platform's guidelines for representing a business | **Confirmed and quoted as conditions**, with the read stamped 2026-08-02 in `gbp-checklist.md` §1 following the D26 pattern. The file states that the step re-reads rather than citing that table as current |
| Suite-designator differences are widely reported to matter little to how the engine resolves one business from another, while inconsistent strings across a business's own surfaces erode trust and can misplace a map pin | Search: GBP address mismatch, suite number, effect on ranking | **Confirmed as split**, and encoded as split. `canonical-nap-record.md` §5 states that both halves are hearsay about an unobservable system, that what is observable is that the strings disagree, and that no class of difference is dismissed as harmless on that basis |
| Accuracy across fewer citation sources outperforms volume across many; data aggregators redistribute a record to a long tail of directories; tier-1 platforms are the map, search and major consumer directories | Search: local citation building 2026, quality over quantity, data aggregators | **Confirmed** for the direction and for the aggregator mechanism, which the source material omits entirely and which is added here. Every quantity attached to it was rejected — D40 |
| Near-duplicate location-page sets are treated as scaled content abuse and can be deindexed as a set, and enforcement has tightened rather than relaxed | Search: location and service-area pages, doorway pages, 2026 policy | **Confirmed** for the constraint. Four numbers found alongside it — a duplicate-detection threshold, a required share of unique content, a publishing rate, a city count — were rejected as unsourced thresholds, and the constraint is encoded without any of them |

## Drift control

- **Scope-expansion proposals recorded but NOT implemented:** three.
  1. Review checking — ratings, velocity, and replies (D44). Externally validated as the second-heaviest local signal at roughly 16%, so the gap is real. Not implemented: it needs `architecture.md` §5 approval, and its lifecycle calls for a separate unit rather than a field inside a snapshot record.
  2. A `local_presence.service_areas` list in the schema (D45). The Page Plan needs it on every run and it arrives from the operator every run.
  3. An optional output-directory key for this Skill's record (D45), matching `research_output.path` and `architecture_output.path`. Neither existing key was reused.
  Nothing else. Review management, reputation monitoring, post and offer scheduling, listing-submission automation, duplicate-removal requests, questions and answers, messaging, profile performance insights, programmatic location-page generation from a dataset, and on-page auditing were all encountered in package 28 or in the external guidance and all rejected rather than carried in as essential. See the D36 ledger and `gbp-checklist.md` §4.
- **Shared-layer problems recorded but NOT edited:** two, both recorded as the D45 proposals above and neither acted on. `project-config.schema.yaml` has no key for the service areas a business serves and no output-path key for this Skill. Beyond the single authorised commit `f96805a`, no shared-layer file was modified: `references/policy-kernel.md`, `references/skill-contract.md`, `docs/architecture.md` and `project-config.schema.yaml` were read in full and no further problem was found in any of them. `docs/architecture.md` §1 lists `scripts/validate-skill.sh`, which does not exist; `VERSIONS.md` already records it as not yet present, so it is a known open item rather than a new finding, and it was not created here.
- **Neither of the other two Skills was revisited.** `seo-geo-research` and `content-strategy-architect` were read in full as boundary context and neither was modified. Two interface points were checked and found already correct: research step 10 flags a local-pack-dominant SERP for this Skill and does not act on it, and architecture's `Hands off to` already names `local-presence-manager`. This Skill reads only the local-pack column of the pack's GEO surfaces table, optionally, and treats it as evidence a term is served locally rather than as a demand figure.
- **Settled decisions whose "reverses if" condition may be met:** none. Two were checked specifically. **D4's** condition — a consuming client with genuinely contested entity identity across many locations or brands — did **not** fire, and the run found a positive reason for the rejection rather than merely no reason against it: the unit's real problem is one set of three strings written down in several places, some of them stale, which is a dated flat snapshot and not an event stream. That reasoning is recorded in D36 and stated inside the Skill at `observation-label-map.md` §5. **D1's** condition did not fire either; package 28's local material was read closely, its play sequence and tier list were genuinely useful and were accepted rewritten, and its two encoded numbers were both wrong to carry — one a wording instruction, one an unsourced threshold.
- **Contract rules re-checked before commit:** `skill-contract.md` §2 confirmed — frontmatter complete, with a negative boundary naming all three neighbours: `seo-geo-research`, `content-strategy-architect`, and the voice Skill. §3 confirmed — all six required sections present, in order (Skill Contract → Data sources → Decision gates → Procedure → Output → Handoff summary). §4 confirmed — all sixteen `Done when` items are checkable by looking at the record without judgement, and item 16 makes the check fire unconditionally by requiring the sixteen-row check table to be written every run, pass or fail. §6 confirmed by scan of all six authored files: no client name, display name, service, city, address, phone digits, domain, plugin, tool, or project path appears in any of them; every project value is read from a named config key, and the tier-5 citation rows are placeholders the operator fills for exactly this reason. §7 confirmed — long tables, taxonomies and templates live in `references/`, and `SKILL.md` reads end to end.

## Validation test

**D10 case: the consuming project's NAP state. Result: pass, with one declared limitation.**

**Method.** The drafted Skill was executed against the consuming project at its own path and against its live site. The project has no installed `project-config.yaml` for this bundle, so `local_presence.canonical_nap` read `missing` and stop-and-ask gate 2 fired — putting the run on the observation-only path, which is what exposed the fault below. Step 2 was run as written: discover every source that states a NAP, read the site first, then the profile, then the rest.

**What the run observed, before opening any of the project's conclusions.** The live site, fetched during the run, states the address identically on its home and contact pages. Two of the site's stored NAP records — its cookie-compliance company address and its sitewide local-business schema — carry the same string. The same two stores, in their pre-change backups, carry a **different unit designator**, which establishes that the site was moved from one designator to the other and dates the move. A search of the public index renders the same address with the street type spelled out where every site surface abbreviates it.

**The finding, reached without being told where to look.** The profile and the website disagree on **one word of the address**: the unit designator. The site says one form on all its surfaces; the profile still says the other. The comparison is `words-differ` under `canonical-nap-record.md` §5, and it fires mechanically from two rows of the Observed Sources table.

**The limitation, declared.** The profile side of that comparison is **not** a live read. No profile export, dashboard screenshot, or reachable public listing was available to this session, so the profile string came from the project's own dated record of it — located by searching for profile sources during step 2, not by searching for the answer. Under the Skill's own rules that row is carried with its original date and marked `not re-observed this run`, and the profile's current state goes in the Unknowns table. The comparison is therefore against a four-day-old observation and the record has to say so. That requirement is D43, and it exists because of this run.

**Two faults the validation caught in the draft.** Both are the kind that only appear when the Skill is run rather than read.

1. **The comparison was excused on exactly the run that needed it.** The draft hung the whole variance table off the canonical NAP, and let `Done when` items 4, 5 and 6 read `n/a` on an observation-only run. A consuming project with no declared canonical — this one — would therefore have produced a transcription table containing both strings and no comparison between them, leaving the central finding for a reader to spot by eye. Fixed: the comparison now runs against a designated base named in the record, items 4–6 are never `n/a`, and only items 3, 11 and 12 may be. Recorded as **D42**. This is `docs/decisions.md` D29's fault in a second Skill, and the underlying error is identical — treating a decision as a precondition of the observations that inform it.
2. **The draft had no rule for a stale observation**, so the only profile evidence available was either going to be presented as current or thrown away. Fixed as **D43**, with a continue-silently gate, a label-map row, and a template line.

**A finding the project's own records do not carry as open.** The divergence is recorded in the project's history and in its master handoff, but the same-day supersession that created it is not in the report's own open-items list. The Skill's Remediation list produces it as an open row every run, because a `words-differ` variance against a tier-1 source is a remediation row by construction rather than by whether someone remembered to carry it forward.

**A second variance the project has never compared.** Every site surface abbreviates the street type; the public index renders it spelled out. The Skill records this as an observation with its surface and date, and classifies the source as `Unknown` pending a direct read, because a search-result rendering is a synthesised surface and may be normalising. It is a candidate finding, honestly labelled, not a claim.

**The control that would have prevented the original divergence.** Stop-and-ask gate 3. The profile was aligned to one designator and the site was moved to the other, by two separate instructions on the same day, each correct in isolation. A canonical agreed once, with a source that disagrees becoming a Remediation row rather than a silent edit in either direction, is exactly what stops the second instruction from undoing the first.

## Open for the coordinating agent

1. **Review checking is a real gap and needs a scope decision.** D44 records it, `gbp-checklist.md` §4 states it in the Skill, and the external validation half of `architecture.md` §5's scope-expansion rule is done: review signals are reported at roughly 16% of local pack weight, second only to profile signals. What is missing is the explicit operator approval and, if granted, a decision on shape — the recommendation here is a **separate unit** with its own completion criterion, not a field inside this Skill's snapshot, because a review count written once into a record nothing updates is the state-column rot D30 already documented. This Skill is complete without it and does not claim otherwise.

2. **Three path-shaped config keys now, and the pattern is worth settling once.** D45 proposes `local_presence.service_areas` and an output-directory key for this Skill's record. The second is the third such key in three Skills — `research_output.path` (D22), `architecture_output.path` (D35), and now this one — each added separately and each deliberately not reusing its predecessor. That reasoning was right each time, and three instances is the point at which a single convention for "where does this Skill's record go" is cheaper than a fourth debate. Not implemented here; the schema is shared layer and this task's authority covered one commit of edits already on disk.

## Commit

`<hash>` — `feat: author local-presence-manager skill and its reference layer`

Preceded in this session by one fix commit carrying the authorised shared-layer work:

- `f96805a` — `fix: correct D11-D23 dates and add architecture_output.path (D34, D35)`

The feature commit carries every deliverable: the Skill, its six reference files, D36–D45, the `VERSIONS.md` update, and this report. **Not tagged**, per the brief — tagging is a separate task once all three Skills have passed.

A report cannot contain its own commit hash: writing the hash in changes the tree and so changes the hash. This line names the commit containing the deliverables and is corrected by a one-line follow-up commit that contains nothing else.
