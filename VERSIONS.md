# Versions

One version for the whole bundle. All Skills share it.

A release requires a **stated reason grounded in a real finding** — a defect met in practice, a validated methodology change, or a capability that was actually requested. Tidiness is not a reason.

Installed copies in consuming projects are byte-identical to a tag and are never edited in place.

---

## Unreleased

Shared reference layer in place. One of three Skills authored.

Skill files carry `version: 0.0.0-unreleased` in frontmatter until the first tag is cut (`docs/decisions.md` D19).

**Present:**

- `references/skill-contract.md` — authoring and execution contract
- `references/policy-kernel.md` — non-negotiable evidence, authority, and stopping rules
- `project-config.schema.yaml` — consumer configuration contract
- `CLAUDE.md` / `AGENTS.md` — agent routing
- `docs/architecture.md`, `docs/decisions.md`, `docs/run-reports/`
- `skills/seo-geo-research/SKILL.md` + six reference files

**Not yet present:**

- `skills/content-strategy-architect/SKILL.md`
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

No tag will be cut until all three Skills pass their validation case in `docs/decisions.md` D10.
