# Versions

One version for the whole bundle. All Skills share it.

A release requires a **stated reason grounded in a real finding** — a defect met in practice, a validated methodology change, or a capability that was actually requested. Tidiness is not a reason.

Installed copies in consuming projects are byte-identical to a tag and are never edited in place.

---

## v1.0.1 — 2026-08-02

All three Skills carry `version: 1.0.1` in frontmatter.

**Reason for the release.** The first production run of the bundle — `seo-geo-research` into `content-strategy-architect`, against a real cluster in a consuming project — **found four faults, three of which were contradictions or gaps that forced the operator to interpret rather than follow.** A step that required output from a step that had not run yet. A `Done when` item that made one of its own gate's options unreachable. An input state that no rule on either side of the handoff defined. And an enforced count with no definition, which the run had to define for itself before it could report `Pass`.

None of the four blocked the run. Every one of them was survivable only because a careful operator interpreted the Skill and said so. That is precisely the failure mode `Done when` exists to prevent, so it is a release reason.

Run report: `docs/run-reports/2026-08-02-v1.0.1.md`. Decisions: D52 (the specification), D55–D58 (the calls made carrying it out).

### The contract change

`references/skill-contract.md` §3 now requires that **each procedure step names its inputs, and no step may name an output produced by a later step** — checkable from the `SKILL.md` alone.

This is the third sequencing fault the bundle has shipped: one in each Skill (D29, D42, D52), and all three found by execution rather than by any of the conformance passes that read them. Three for three is a pattern, not coincidence. The check now fires at authoring time.

Applied as a full pass across all three Skills: one fault found, the one D52 named. Every step in all three now declares its inputs — 37 steps — which is what makes the ordering check mechanical rather than a re-reading of prose.

### What changed

| Fault | Where | What was done |
|---|---|---|
| **F2** — step 5 required step 6's output | `seo-geo-research` | Intent classification split in two: step 5 is Pass A from the query, step 6 reads the SERPs, step 7 is Pass B from those reads. Steps renumbered 1–13, and every cross-reference in the Skill and its six reference files re-checked (D55) |
| **F3** — partial SERP observation undefined on both sides | `serp-read-protocol.md` §2, `cannibalization-guardrails.md` §2.1 | `partial` is now a first-class observation state carrying its captured position count. The overlap rule gains a position floor of 8 of the top ten: below it a pair is `Unknown` and never split, and above it a partial read can send a pair to one page but never to two (D56). `Done when` items 7 and 8 in research and item 5 in architecture admit the third state |
| **F5** — an enforced count with no definition | `references/skill-contract.md` §5 | The evidence-basis counting rule is defined once, for all three Skills, with its edge cases named. The Skills are told not to define their own (D57) |
| **F6** — `Done when` item 1 made gate 2 option 3 unreachable | `content-strategy-architect`, and `local-presence-manager` | Item 1 is scoped to required keys whose absence does not have its own gate. The same contradiction existed three times over in `local-presence-manager` and was fixed there too (D58) |
| **F1** — gate 3 read as being about the channel | `seo-geo-research` | Reworded: "…but the named tool cannot actually be read: not connected, not authenticated, or not reachable" |
| **F4** — "existing page" vs "planning row" ambiguous | `content-strategy-architect` step 2, `primary-keyword-selection.md` §5 | A planning row declaring a primary keyword is an inherited decision **even when no page exists**, stated explicitly. The Inherited Decisions table names which kind each row is. The first run found three undocumented decisions this way on a green-field cluster |

**Deferred, unchanged:** F7 (per-member selection trails — a template improvement with a working alternative in place) and F10 (no staleness threshold on the schema snapshot — needs a real second read before a threshold can be chosen honestly). Review checking stays deferred to v1.1 (D44, D48).

### Declared limitations

Carried forward from v1.0.0 and still standing:

| Skill | What is still not validated |
|---|---|
| `seo-geo-research` | The tool-fed path. The D10 validation pack's universe was 53 observed terms against a 204-term export, and the first production run was zero-tool by operator direction at gate 3 — so every demand metric was `Unknown` and sources 2, 6 and 7 have still not run against real data |
| `local-presence-manager` | The profile side of the NAP comparison is not a live read. No profile export, dashboard screenshot, or reachable public listing was available; the profile string came from the project's own dated record of it. This Skill was not exercised by the first production run |

**Closed since v1.0.0:** `content-strategy-architect`'s pack-consuming path. The first production run exercised primary-keyword selection from a real pack, the cluster map, the link map, the schema table and three briefs. D51's condition is met.

New with this release, and honest about it:

- **The planning-record write has still never run.** Gate 2 stopped it by design in the first production run, and the record it produced lists the fifteen intended cell-writes. It needs a consuming project with a stable row-identifier column before it is exercised.
- **The partial-observation machinery is written, not exercised.** F3's rules — the `partial` state, the captured position count, the position floor of 8 — were derived from a run that had to improvise past their absence. No run has yet followed them.

---

## v1.0.0 — 2026-08-02

First release. All three Skills carry `version: 1.0.0` in frontmatter (`docs/decisions.md` D19).

**Reason for the release.** All three Skills passed their D10 validation case against real production data, and a consuming project is ready to install. Both halves are required: D10 gates the tag on validation, and a bundle nobody is installing has no reason to be tagged.

### Declared limitations

Each Skill passed with a limitation its own run report declares. They are collected here so an installer sees all three without opening three reports.

| Skill | What was not validated | Why it is a limitation and not a defect |
|---|---|---|
| `seo-geo-research` | The validation pack's universe is 53 observed terms against the archive's 204-term export. The seven tool screenshots supplied show each panel's total but only its top five rows, so two terms present in the archive's national table are absent from the pack | Input coverage, not method. The pack declares the shortfall in a universe-coverage caveat and lists it in its Unknowns table rather than presenting 53 as complete. Run against the full CSV export, the universe would not have been narrower |
| `content-strategy-architect` | The pack-consuming path. No `seo-geo-research` pack existed for the validation cluster, so gate 3 fired and the case ran as a **re-verification-only run**. Primary-keyword selection, the cluster map, the link map, the schema table, the briefs and the planning write were not exercised against real data | The run validated what it could reach, and reached a real finding there: 35 of 35 rows carry a declared primary keyword and none carries a snapshot date, source, or rejected alternatives. The gate behaved correctly. The untested path is untested, not known-broken |
| `local-presence-manager` | The profile side of the NAP comparison is not a live read. No profile export, dashboard screenshot, or reachable public listing was available, so the profile string came from the project's own dated record of it — a four-day-old observation | The Skill's own rules handled it: the row is carried with its original date, marked `not re-observed this run`, and the profile's current state goes to the Unknowns table. That requirement is D43 and it exists because of this run |

One further limitation applies to the bundle rather than to any Skill: **review checking is not present.** External validation reports review signals as roughly 16% of local pack weight, second only to profile signals. The gap is accepted on merit and deferred to v1.1 as a separate unit with its own completion criterion, not as a field inside the local-presence record (D44, D48).

**Present:**

- `references/skill-contract.md` — authoring and execution contract
- `references/policy-kernel.md` — non-negotiable evidence, authority, and stopping rules
- `project-config.schema.yaml` — consumer configuration contract
- `CLAUDE.md` / `AGENTS.md` — agent routing
- `docs/architecture.md`, `docs/decisions.md`, `docs/run-reports/`
- `skills/seo-geo-research/SKILL.md` + six reference files
- `skills/content-strategy-architect/SKILL.md` + eight reference files
- `skills/local-presence-manager/SKILL.md` + six reference files

**Not yet present:**

- `scripts/validate-skill.sh`

### Added 2026-08-03 — `seo-geo-research`

Produces a labelled evidence pack for one service or topic area and recommends nothing. Twelve mechanically-checkable `Done when` items, both decision-gate lists populated, three `research_tools.access_mode` values supported, and a complete zero-tool path.

Reference files: `keyword-universe-sources.md`, `intent-classification.md`, `serp-read-protocol.md`, `metric-label-map.md`, `competitor-and-gap-mapping.md`, `evidence-pack-template.md`.

Decisions recorded: D11–D20. Three are methodology changes rather than codified past practice, each externally validated and flagged as an addition per the D9 pattern:

- **D13** — SERP composition is `Measured` or `Unknown`, never `Estimated`.
- **D14** — a tool-reported zero volume is `Unknown`, never a demand figure.
- **D15** — intent is classified twice and the SERP read wins on disagreement, with a sub-intent layer added.

D10 validation case run: Gut Health, **pass with one declared limitation** — see `docs/run-reports/2026-08-03-seo-geo-research.md`.

### Fixed 2026-08-02 — shared-layer gaps raised by the `seo-geo-research` run

`references/skill-contract.md` §5 enumerated four of the five evidence labels the policy kernel defines; `Calculated` added (D23). `project-config.schema.yaml` gained an optional `research_output.path` (D22). D21 confirmed the Search Console boundary, drawn at the operation rather than the data source. A worked example in `intent-classification.md` named a real client service and city, violating `skill-contract.md` §6, and was de-identified.

Consequent to D23, `seo-geo-research` dropped its local convention of folding `Calculated` under the weakest label among a value's inputs and now counts `Calculated` directly.

### Added 2026-08-02 — `content-strategy-architect`

Consumes one evidence pack and produces one cluster architecture: a primary keyword with its trail, a pillar and its members, a cannibalization pass, a link map, a schema type per page, a brief per page to be written, and the planning-record rows. Sixteen mechanically-checkable `Done when` items, eleven stop-and-ask gates and ten continue-silently gates, and a complete path when the pack carries `Unknown` in critical fields.

Reference files: `primary-keyword-selection.md`, `cluster-architecture.md`, `cannibalization-guardrails.md`, `internal-link-map.md`, `schema-decision.md`, `content-brief-template.md`, `planning-record-protocol.md`, `cluster-record-template.md`.

Decisions recorded: D24–D33. Four are methodology changes rather than codified past practice, each externally validated and flagged as an addition per the D9 pattern:

- **D26** — schema recommendations separate documented rich-result eligibility from entity value, and both `FAQPage` and `Service` are `no` on the first.
- **D27** — aggregate cluster demand is reported as a floor, never as a total.
- **D28** — one page or two is decided by observed SERP overlap, and an unobserved pair is never split.
- **D30** — the planning record gets a write rule per stage this bundle owns, and state fields are not written at all.

D10 validation case run: Hormone Health, **pass** — the Skill flagged the missing numeric snapshot on all 35 rows of the cluster without being told to look for it. The run also caught a sequencing fault in the draft, fixed as D29. See `docs/run-reports/2026-08-02-content-strategy-architect.md`.

### Added 2026-08-02 — `local-presence-manager`

Establishes what one business location's presence is: one canonical NAP agreed once, a thirteen-item Google Business Profile checklist, a citation list carrying a status per source, and a location and service-area page plan. Sixteen mechanically-checkable `Done when` items, ten stop-and-ask gates and thirteen continue-silently gates, and a zero-tool path that is the normal path rather than a degraded one. Changes nothing live: no profile edit, no listing submission, no publication, no spend.

Reference files: `observation-label-map.md`, `canonical-nap-record.md`, `gbp-checklist.md`, `citation-sources.md`, `location-page-plan.md`, `local-presence-record-template.md`.

Decisions recorded: D36–D45. Four are methodology changes rather than codified past practice, each externally validated and flagged as an addition per the D9 pattern:

- **D37** — the website is a NAP source, and every place it states a NAP is its own row. The source material audits the profile and the directories and never reads the site.
- **D38** — an unchecked source is `Unknown`, never `missing`, and no local-presence observation is ever `Estimated`.
- **D42** — the variance comparison runs without a canonical, against a named comparison base.
- **D43** — a dated observation from an earlier session is carried with its date, never as current and never discarded.

D40 rejects six unsourced thresholds found in the source material and in current external guidance, and keeps only the direction underneath them. D44 records the review-signal gap — externally validated as the second-heaviest local factor — as a proposal rather than filling it.

D10 validation case run: the consuming project's NAP state, **pass with one declared limitation** — the Skill reached the known one-word site-versus-profile address mismatch without being told where to look, and caught a sequencing fault in the draft, fixed as D42. See `docs/run-reports/2026-08-02-local-presence-manager.md`.

### Fixed 2026-08-02 — release preparation

`project-config.schema.yaml` consolidated `research_output.path` and `architecture_output.path` into one `outputs:` block carrying one key per Skill, with the no-sharing rule written into the block rather than re-derived per Skill (D46). Done before any consumer is installed, when the change costs two key renames instead of a migration. All three Skills now name their own key. `local_presence_extra.service_areas` added and wired into the location page plan (D47).

A pre-release conformance pass over all three `SKILL.md` files and all twenty reference files against `references/skill-contract.md` found `§2`, `§3`, `§4` and `§7` clean, and two `§6` failures in the shared layer: `references/policy-kernel.md` named a real consuming client's voice Skill in its worked example, and `project-config.schema.yaml` carried one real client's id, display name, canonical host, locality and service areas in its `example:` fields. Both de-identified. Full result in `docs/run-reports/2026-08-02-v1.0.0-release.md`.

Review checking was approved in principle and deferred to v1.1 (D48).
