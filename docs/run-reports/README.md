# Run Reports

One file per completed work session, committed with the work it describes.

**Path:** `docs/run-reports/YYYY-MM-DD-<task-slug>.md`
Example: `docs/run-reports/2026-08-03-seo-geo-research.md`

## Why this exists

Work on this bundle is split across two agent surfaces: a coordinating session that holds project memory and writes the briefs, and an execution session that does the authoring. Neither can read the other's transcript.

A run report is the handoff. It is written by the executing agent, committed to the repository, and read directly by the coordinating agent. Nothing is relayed by hand.

Reports are also the permanent record of *how* a decision got made, which `docs/decisions.md` deliberately does not carry — that file records what was decided and why, not the path taken to it.

## Required structure

```markdown
# Run Report — <task> — YYYY-MM-DD

## Brief
<one paragraph: what was asked>

## Handoff summary
<the exact block from references/skill-contract.md §5>

## Delivered
| File | New/Modified | What it contains |

## Decisions recorded
| ID | Decision | Accept/Reject | Basis |

## External validation
| Claim encoded | Source consulted | Outcome: confirmed / contradicted / inconclusive |

## Drift control
- Scope-expansion proposals recorded but NOT implemented:
- Shared-layer problems recorded but NOT edited:
- Settled decisions whose "reverses if" condition may be met:
- (state "none" explicitly where none — silence is not a result)

## Validation test
<the D10 case run, and its result — pass, partial, or fail with reason>

## Open for the coordinating agent
<anything needing a judgement call outside this task's authority>

## Commit
<hash and message>
```

## Rules

- **Write it even when the run was clean.** "Swept, found nothing" is a result; silence is not.
- **Never edit a past report.** It records what was true when written. Corrections go in the next report.
- **`Status: partial` is a legitimate outcome.** An honest partial beats a gap filled with an estimate.
- **State "none" explicitly** in each drift-control line rather than omitting the line.
