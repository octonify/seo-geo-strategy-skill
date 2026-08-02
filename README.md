# SEO/GEO Strategy Skill

A portable Skill bundle for the **strategy layer** of search content work: keyword and SERP research, topic-cluster architecture, and local search presence.

It is deliberately **upstream-only**. It decides *what* to publish, *why*, and *how the pieces relate*. It never writes body copy, never touches a CMS, and never generates media.

## What this bundle owns

| Skill | Responsibility |
|---|---|
| `seo-geo-research` | Keyword universe, intent classification, SERP reading, competitor and content-gap analysis. Produces labelled evidence, not decisions. |
| `content-strategy-architect` | Primary-keyword selection with a mandatory evidence trail, pillar/cluster architecture, cannibalization guardrails, internal-link map, schema decision. Produces the content brief and the planning-database row. |
| `local-presence-manager` | Canonical NAP record, Google Business Profile optimization, citation priority, location and service-area page plans. |

## What this bundle does not own

| Concern | Owner |
|---|---|
| Writing body copy, brand voice, domain safety rules | The consuming project's own `{client}-content-voice` Skill |
| Visual design and prototypes | The consuming project's design process |
| CMS/page-builder implementation | The consuming project's implementation Skill |
| Image and media generation | The consuming project's asset Skill |

The handoff boundary is the **content brief**. This bundle produces it; a client-specific voice Skill consumes it.

## Consuming this bundle

A consuming project installs a tagged release and supplies its own `project-config.yaml`. No project-specific value ever lives inside a Skill file.

```
<consumer-project>/.claude/Skills/seo-geo-strategy/
  ├── (installed files, byte-identical to the release tag)
  ├── project-config.yaml      ← the only project-specific file
  └── INSTALLED-VERSION.txt    ← pinned tag
```

Required config fields are defined in [`project-config.schema.yaml`](project-config.schema.yaml). The most important is `authority_override_skill`: the name of the client's voice/safety Skill, which always outranks any recommendation this bundle makes about language, claims, or tone.

**Onboarding prerequisite:** a consuming project must already have a `{client}-content-voice` Skill. Without it, the chain breaks at the brief handoff and no copy can be produced.

## Documentation

- [`docs/architecture.md`](docs/architecture.md) — structure, boundaries, install pattern, anti-drift mechanisms
- [`docs/decisions.md`](docs/decisions.md) — every non-obvious design decision, dated, with reasoning
- [`references/skill-contract.md`](references/skill-contract.md) — the execution contract every Skill here obeys
- [`references/policy-kernel.md`](references/policy-kernel.md) — non-negotiable evidence, authority, and stopping rules
- [`VERSIONS.md`](VERSIONS.md) — release history, each entry driven by a real finding

## Status

Pre-release. No tagged version yet. See `docs/decisions.md` for current design state.
