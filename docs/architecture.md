# Architecture

## 1. What this bundle is

Three Skills sharing one contract, one policy kernel, and one version. They cover the **strategy layer** of search content work and stop at the content brief.

```
seo-geo-strategy-skill/
  README.md · LICENSE · VERSIONS.md · .gitignore
  CLAUDE.md · AGENTS.md                  ← routing for agent hosts
  project-config.schema.yaml             ← what a consumer must supply
  references/
    skill-contract.md                    ← authoring + execution contract
    policy-kernel.md                     ← always-on non-negotiable rules
  skills/
    seo-geo-research/SKILL.md
    content-strategy-architect/SKILL.md
    local-presence-manager/SKILL.md
  scripts/
    validate-skill.sh                    ← contract conformance check
  docs/
    architecture.md                      ← this file
    decisions.md                         ← dated design decisions
```

`references/` at the root is shared across all three Skills. Each Skill may also have its own `references/` directory for material only it uses.

## 2. Skill boundaries

The boundaries follow one rule: **two things belong in different Skills when they have different completion criteria.** This is the lesson from a sibling project where a planning database mixed one-time intent data with continuously-changing state data under no write rule — the state columns rotted while the intent columns stayed fine.

| Skill | Unit | Completion criterion |
|---|---|---|
| `seo-geo-research` | One service or topic area | Every candidate carries labelled metrics and an intent class |
| `content-strategy-architect` | One cluster | Every page has an owner, a boundary, and a link target; the primary choice has an evidence trail |
| `local-presence-manager` | One business location | One canonical NAP agreed; GBP checklist complete; citation list has a status per source |

Research produces labelled data and no decisions. Architecture consumes that data and produces decisions with a trail. Local presence is separate because its inputs (NAP, listings) and outputs (profile state, citation list) share nothing with keyword data.

## 3. The handoff chain

```
  ┌─────────────────────┐
  │ seo-geo-research    │  labelled keyword + SERP + competitor data
  └──────────┬──────────┘
             ▼
  ┌─────────────────────────────┐
  │ content-strategy-architect  │  primary keyword + evidence trail,
  └──────────┬──────────────────┘  cluster map, brief, planning row
             ▼
  ┌─────────────────────────────┐
  │ {client}-content-voice      │  ← OUTSIDE this bundle
  └──────────┬──────────────────┘    writes the actual copy
             ▼
      consuming project's package → design → implementation → media
```

`local-presence-manager` runs alongside, feeding the local-intent portion of the architecture decision and producing its own deliverables.

**The bundle never crosses the voice boundary.** It produces a brief. A client-specific `{client}-content-voice` Skill turns that brief into copy. Every consuming project must have one; this is an onboarding prerequisite, not an optional extra.

## 4. Install pattern

Modelled on the sibling `wordpress-elementor-implementation-skill`, which proved this pattern in production.

```
<consumer>/.claude/Skills/seo-geo-strategy/
  <installed files, byte-identical to the release tag>
  project-config.yaml          ← the ONLY project-specific file
  INSTALLED-VERSION.txt        ← the pinned tag
```

Rules:

- The installed copy is **never edited in place**. Changes happen upstream and arrive as a new tag.
- All project-specific values live in `project-config.yaml`. No exceptions.
- Where a consuming project mirrors Skills into a second tree (`.agents/skills/`), both copies must hash identically. Drift is never resolved by taking the newer file; the designated authoritative tree wins.

## 5. Anti-drift mechanisms

Six, each addressing a failure actually observed in a sibling project:

| Mechanism | Failure it prevents |
|---|---|
| Installed copies are read-only, changed only via tag | Local edits that silently diverge from source |
| Config separated from logic from v1.0.0 | A sibling project had to do this retroactively in v1.0.1 |
| Every version needs a stated real-world reason | Churn that makes the version number meaningless |
| `docs/decisions.md` records every non-obvious call | A later session re-litigating settled questions |
| Scope expansion requires external validation + explicit approval | Agent quietly widening the bundle toward the 16-skill reference system |
| `Done when` items must be mechanically checkable | Rules that exist on paper but never fire |

## 6. Explicitly out of scope

Deliberate exclusions, each with a reason:

| Excluded | Reason |
|---|---|
| Writing body copy | Owned by `{client}-content-voice`; domain safety cannot be generalised |
| Technical SEO auditing, Core Web Vitals, crawl analysis | No consumer for it in the current workflow |
| Rank tracking, performance monitoring, backlink analysis | Post-publication measurement; separate lifecycle, separate cadence |
| CMS/page-builder implementation | Owned by the consuming project's implementation Skill |
| Image and media generation | Owned by the consuming project's asset Skill |
| Event-sourced entity registry | Studied and rejected — enterprise-scale identity machinery, mismatched to single-location clients. See `docs/decisions.md`. |

Adding any of these requires the §5 scope-expansion rule: external validation plus explicit operator approval.
