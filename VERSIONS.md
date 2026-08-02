# Versions

One version for the whole bundle. All Skills share it.

A release requires a **stated reason grounded in a real finding** — a defect met in practice, a validated methodology change, or a capability that was actually requested. Tidiness is not a reason.

Installed copies in consuming projects are byte-identical to a tag and are never edited in place.

---

## Unreleased

Scaffold and shared reference layer in place. The three Skills are not yet authored.

**Present:**

- `references/skill-contract.md` — authoring and execution contract
- `references/policy-kernel.md` — non-negotiable evidence, authority, and stopping rules
- `project-config.schema.yaml` — consumer configuration contract
- `CLAUDE.md` / `AGENTS.md` — agent routing
- `docs/architecture.md`, `docs/decisions.md`

**Not yet present:**

- `skills/seo-geo-research/SKILL.md`
- `skills/content-strategy-architect/SKILL.md`
- `skills/local-presence-manager/SKILL.md`
- `scripts/validate-skill.sh`

No tag will be cut until all three Skills pass their validation case in `docs/decisions.md` D10.
