# Versions

One version for the whole bundle. All Skills share it.

A release requires a **stated reason grounded in a real finding** — a defect met in practice, a validated methodology change, or a capability that was actually requested. Tidiness is not a reason.

Installed copies in consuming projects are byte-identical to a tag and are never edited in place.

---

## Unreleased

Shared reference layer in place. Two of three Skills authored.

Skill files carry `version: 0.0.0-unreleased` in frontmatter until the first tag is cut (`docs/decisions.md` D19).

**Present:**

- `references/skill-contract.md` — authoring and execution contract
- `references/policy-kernel.md` — non-negotiable evidence, authority, and stopping rules
- `project-config.schema.yaml` — consumer configuration contract
- `CLAUDE.md` / `AGENTS.md` — agent routing
- `docs/architecture.md`, `docs/decisions.md`, `docs/run-reports/`
- `skills/seo-geo-research/SKILL.md` + six reference files
- `skills/content-strategy-architect/SKILL.md` + eight reference files

**Not yet present:**

- `skills/local-presence-manager/SKILL.md`
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

No tag will be cut until all three Skills pass their validation case in `docs/decisions.md` D10.
