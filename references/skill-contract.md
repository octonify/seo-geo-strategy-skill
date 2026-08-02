# Skill Contract

The authoring and execution contract every Skill in this bundle obeys. [`policy-kernel.md`](policy-kernel.md) is the short always-on projection of the rules below; this file is the full version and the authority when the two appear to differ.

---

## 1. One Skill, one unit of work

Every Skill declares a **unit**: the single thing it operates on. One service page's keyword universe. One cluster architecture. One business location's presence.

If a request spans two units, run the Skill twice. Do not widen the unit mid-run.

---

## 2. Required frontmatter

Every `SKILL.md` carries:

```yaml
---
name: <kebab-case, matches the directory name>
description: >
  Use when the user asks to <trigger phrases>. Produces <output>.
  Not for <the nearest neighbouring skill and what it does instead>.
version: <bundle version, not per-skill>
license: Proprietary
unit: <the single thing this skill operates on>
authority_override: <read from project-config.yaml at runtime>
---
```

The `description` must contain an explicit **negative boundary** naming the nearest neighbouring Skill. Without it, two Skills with similar triggers will both fire and produce contradictory output.

---

## 3. Required sections, in order

Every `SKILL.md` has these sections. None is optional.

### `## Skill Contract`

Five declarations:

- **Unit** — the one thing operated on.
- **Reads** — every input, and where it comes from. Name the config keys used.
- **Writes** — every output file or record, with its path pattern.
- **Done when** — a numbered checklist. See §4.
- **Hands off to** — the next Skill, or the operator, and what they receive.

### `## Data sources`

What tools are used, and — critically — what the Skill does when none are connected. Every Skill in this bundle must be able to run from operator-pasted data. A Skill that only works with a paid tool connected is not acceptable.

### `## Decision gates`

Two headed lists, per policy kernel §4:

- **Stop and ask** — each entry states the condition and the numbered options presented.
- **Continue silently** — each entry states the condition and the default applied.

### `## Procedure`

Numbered steps. Each step states its **inputs** and its **output**. Steps that produce a labelled metric state which evidence labels are acceptable for that step.

**No step may name an output produced by a later step.** A step's inputs are the config keys read at step 1, the operator's material, an observed surface, or the output of a step with a lower number. Naming anything else makes the step impossible to follow at the point it is asked for, and the run either stops or silently reorders itself.

This is checkable from the `SKILL.md` alone: read the `Procedure` top to bottom, and for every step ask which earlier step or which declared input produces each thing it names. A step naming something no earlier step produced is a defect in the Skill, and it is fixed by splitting the step or by renumbering — never by leaving the executing agent to work out the real order.

Three of these shipped undetected — one in each Skill (`docs/decisions.md` D29, D42, D52) — and all three were found by execution rather than by reading. The check is written here so it fires at authoring time instead.

### `## Output`

The exact shape of the deliverable, as a template or table skeleton. Not a description of it.

### `## Handoff summary`

The fixed block emitted at the end of every run. See §5.

---

## 4. `Done when` must be mechanically checkable

This is the most important rule in this contract.

An item on a `Done when` list must be verifiable by looking at the output, without judgement.

| Acceptable | Not acceptable |
|---|---|
| "Every shortlisted keyword carries a volume, a difficulty, an intent class, and an evidence label, or an explicit `Unknown` with a reason." | "Keyword research is thorough." |
| "The rejected-alternatives table has at least two rows, each with the metric that caused rejection." | "The decision is well reasoned." |
| "Every cluster member names its parent pillar and states one boundary sentence." | "Cannibalization has been considered." |

**A rule is not enforced until a checklist item fires unconditionally.** A check that only runs when the agent remembers to run it is documentation, not enforcement.

A corollary learned the hard way in a sibling project: validating an output against an authority that can itself be wrong is not validation. Where a check compares two records, state which one wins when they disagree, and check both against the underlying reality where one exists.

---

## 5. Handoff summary

Every run ends with this block. Fixed shape, so a downstream Skill or a later session can parse it.

```markdown
### Handoff summary

- **Skill:** <name>
- **Unit:** <what was operated on>
- **Status:** complete | partial | stopped
- **Produced:** <artifact paths or record identifiers>
- **Evidence basis:** <n Measured, n User-provided, n Calculated, n Estimated, n Unknown>
- **Assumptions:** <each assumption made without asking, or "none">
- **Open questions:** <each unresolved item, or "none">
- **Recommended next:** <one skill name, or "return to operator">
```

`Status: partial` is a legitimate, non-embarrassing outcome. Reporting a partial result honestly is always preferred over filling a gap with an estimate.

### The evidence-basis counting rule

Every Skill's `Done when` list requires the evidence-basis totals to equal the count of labelled values in the deliverable. **This is the definition of one labelled value, and it is the same for all three Skills.** Without one fixed rule, two operators produce two different counts from the same deliverable and both report `Pass` — an enforced check with no definition is worse than no check, because it reads as enforcement.

**One labelled value is one occurrence of one of the five label words — `Measured`, `User-provided`, `Calculated`, `Estimated`, `Unknown` — at a position where it labels a value.** Occurrences are counted, not rows and not distinct labels.

An occurrence counts when it appears in:

- a `Label` cell, or an equivalently-headed cell, of a filled table row — one count for that row;
- a value cell, where the label is written beside the value it labels (`120 — Measured`, `Unknown — tool reports 0 for <locality>`) — one count per such cell;
- a line of prose or a list item that states the label for one named value (`Cluster demand (local): floor 340 across 5 of 9 members — Calculated`).

An occurrence does **not** count when it appears in:

- a section heading, a column heading, or a sentence stating a rule about labels;
- rule text, guidance, or an explanation of what a label means;
- the handoff summary block itself, including the evidence-basis line;
- the `Done when` check table;
- a quoted template, skeleton, or worked example carried into the deliverable.

Consequences worth stating, because they are where two operators would otherwise diverge:

- A table row with a `Label` cell reading `Measured` and two value cells reading `Unknown — <reason>` counts **three**: one for the row's label cell, one for each labelled value cell.
- A row whose `Label` cell is empty counts nothing, and is a defect in the row rather than a zero.
- `Unknown` is counted exactly like the other four. It is a label, not the absence of one.
- The count is over the deliverable as emitted — the pack or the record — and not over the session, the working notes, or anything the deliverable does not contain.

The rule is deliberately mechanical: a second operator counting the same file reaches the same five numbers, and where the deliverable is a file the count is reproducible by searching it. A Skill that states its own counting rule beside the totals is stating something this contract has already decided, and the two can then disagree.

---

## 6. Configuration, never hardcoding

No Skill file contains a client name, domain, service name, city, tool name, brand term, or file path belonging to a consuming project.

Every such value is read from `project-config.yaml` at runtime, and the Skill names the exact config key it reads. If a required key is missing, the Skill stops and names the key — it does not assume a default.

The single exception is the structural key `authority_override_skill`, which every Skill reads and every Skill must honour per policy kernel §1.

---

## 7. Reference files

Long tables, taxonomies, formulas, worked examples, and templates live in `references/` next to the `SKILL.md` that owns them, and are linked from the `Procedure` step that needs them.

The `SKILL.md` itself stays readable end to end. If it cannot be read in one sitting, it is doing too much and should be split or its detail pushed into a reference file.

---

## 8. Versioning

The bundle carries one version. All Skills share it.

A new version requires a **stated reason grounded in a real finding** — a defect met in practice, a validated methodology change, or a new capability that was actually requested. Version bumps for tidiness are not made.

Every release is recorded in `VERSIONS.md` with its reason. Installed copies in consuming projects are byte-identical to a tag and are never edited in place.
