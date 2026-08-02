# Versions

One version for the whole bundle. All Skills share it.

A release requires a **stated reason grounded in a real finding** — a defect met in practice, a validated methodology change, or a capability that was actually requested. Tidiness is not a reason.

Installed copies in consuming projects are byte-identical to a tag and are never edited in place.

---

## Unreleased

Shared reference layer in place. All three Skills authored.

Skill files carry `version: 0.0.0-unreleased` in frontmatter until the first tag is cut (`docs/decisions.md` D19).

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

No tag will be cut until all three Skills pass their validation case in `docs/decisions.md` D10. **All three have now reported a pass**, each with its limitations declared in its run report. Cutting the first release is a separate task: it replaces `0.0.0-unreleased` across three `SKILL.md` files (D19) and needs a stated reason in this file. Nothing here is tagged.
