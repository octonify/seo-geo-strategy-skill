# Planning Record Protocol

Owned by [`../SKILL.md`](../SKILL.md) step 12. Governed by [`policy-kernel.md`](../../../references/policy-kernel.md) §6, which wins over anything here.

This is the one place in this bundle that writes into a consuming project's own records. It is written to be boring and strict, because the failure it exists to close was neither.

---

## 1. The failure this closes

A planning database in a consuming project was read constantly and written to almost never. It had no write rule for any lifecycle stage except the last, so a row was created, consulted for months, and updated only when the work was finished — if then. The fields that recorded a decision stayed accurate because nobody had reason to change them. The fields that recorded state rotted, because the moment they became wrong was never anybody's cue to act.

Two rules follow, and they are the spine of this file:

1. **A write point is named for every stage this bundle owns**, not only the last one.
2. **Stages this bundle does not own are named too**, so the gap after handoff is visible rather than silent.

---

## 2. Preconditions — all three, before anything is written

| # | Precondition | If it fails |
|---|---|---|
| 1 | `planning_record.path` is set and the file at it can be read | Stop-and-ask gate 1. Name the key |
| 2 | `planning_record.row_identifier_field` is set, **and** a column of that name exists in the file | Stop-and-ask gate 2. This is a blocking gap |
| 3 | `planning_record.owned_fields` is set and every field in it exists in the file | Stop-and-ask gate 1, naming the fields that are absent |

**Precondition 2 is the one that stops the run.** A project whose planning record has no stable identifier column cannot be written to safely, and the Skill stops rather than proceeding.

**Title similarity is never a fallback.** Not for a close match, not for an exact string match on a title column, not "there is obviously only one candidate". Titles are edited, duplicated across clusters, and reused between a draft and its replacement. Matching on one silently writes a decision onto the wrong page, and the write leaves no trace that it was a guess. Policy kernel §6 forbids it; this file adds no exception.

When precondition 2 fails, the architecture record and the briefs are still produced in full. Only the write is `stopped`, and the handoff summary says so.

---

## 3. Identifying the row

For each page in the Cluster Map, in this order:

1. Determine the page's identifier value under `planning_record.row_identifier_field`.
   - For an existing page: read it from the inventory. It is the value already in that row.
   - For a page with disposition `create`: the identifier does not exist yet. Construct it by the rule the column's existing values visibly follow, and state that rule in the record.
2. Search the file for that identifier value.
3. Act on what the search returns:

| Result | Action |
|---|---|
| Exactly one row | That is the target row |
| No row, and disposition is `create` | Create one row, carrying the identifier and the owned fields only |
| No row, and disposition is `extend`, `keep`, or `retire` | Stop. The page exists but its row does not; that mismatch is a finding, not something to fix by creating a row |
| More than one row | Stop. Ambiguous identity is precondition 2 failing in practice. Report both rows |
| The identifier rule for a `create` page cannot be determined from existing values | Stop. Do not invent an identifier scheme |

No step in this list falls back to a title, a slug, a URL, or a keyword.

---

## 4. What may be written

**Only fields named in `planning_record.owned_fields`.** Every other column belongs to another layer and is never written, never cleared, never reformatted, and never "tidied" in passing.

Before writing, classify each owned field:

| Field kind | Description | This bundle |
|---|---|---|
| **Intent** | Decided once, stays true — the primary term, the cluster, the page role, the boundary, the schema type, where the evidence trail lives | Writes it |
| **State** | Changes after this bundle stops touching it — anything that tracks progress, position, traffic, or status after handoff | Does **not** write it. Records a finding |

A state field inside `owned_fields` is the exact configuration that produced the original failure: this bundle would set it once, at the only moment it is present, and then the value would rot with no owner. Where one appears, write the finding into the record and leave the field alone:

```
Finding: planning_record.owned_fields names <field>, which tracks state that
changes after this bundle hands off. Not written. The layer that owns the
stage this field describes should own the field.
```

That is a shared-layer observation, and it is reported, not resolved here.

---

## 5. The write points

Two, and both are inside this Skill's own stages.

| # | Write point | When it fires | Fields written |
|---|---|---|---|
| 1 | **Cluster decided** | End of step 8, after the ownership check passes | Owning primary term; cluster or pillar the page belongs to; page role; disposition; boundary sentence; the date; this Skill's name; where the evidence trail is recorded |
| 2 | **Brief produced** | End of step 11, for pages with disposition `create` or `extend` | Schema type decided; where the brief is recorded; the date; this Skill's name |

Both fire in the same run when the run completes. They are separate points because a run that stops between them must leave the record in a state that says so — write point 1 written, write point 2 not, and the handoff summary reporting `partial`.

**Stages this bundle does not own**, named so the gap is visible:

| Stage | Owner |
|---|---|
| Copy written from the brief | The Skill in `authority.authority_override_skill` |
| Page built and published | The consuming project's implementation Skill |
| Anything after publication | Outside this bundle entirely (`docs/architecture.md` §6) |

This bundle writes no field belonging to those stages, and defines no cadence, workflow, or schedule for them. Naming them is the whole of what is done here.

---

## 6. Every write is stamped and shown

Each write carries the date and the name of the Skill that made it (policy kernel §6). Where the planning record has no column for either, the stamp goes into the record's own Record Writes table and the absence is reported as a finding.

The Record Writes table is written every run, and shows the prior value for every cell touched:

```
| Row identifier | Field       | Prior value | New value   | Written on   | By                         |
|----------------|-------------|-------------|-------------|--------------|----------------------------|
| <identifier>   | <field>     | <empty>     | <value>     | <YYYY-MM-DD> | content-strategy-architect |
| <identifier>   | <field>     | <old>       | <new>       | <YYYY-MM-DD> | content-strategy-architect |
```

`Done when` item 15 checks it: every write appears, and every field named is in `owned_fields`.

---

## 7. Overwriting an existing value

An owned field that is empty is filled without asking. An owned field that already holds a **different** value is stop-and-ask gate 5, always.

The three options presented are: overwrite and record the prior value; keep the existing value and record the divergence as a finding; or stop the write and report partial.

The reason it stops: an existing value in an owned field is a decision somebody made, and this run may be looking at less evidence than they were. Overwriting silently destroys the only record that the two decisions differed — which is the same failure mode the re-verification pass in `primary-keyword-selection.md` §5 exists to detect, arriving from the other direction.

---

## 8. What is never done here

- No row is deleted.
- No column is added, renamed, or reordered.
- No row is created for a page that already exists under a different identifier.
- No field outside `owned_fields` is touched, including to correct something obviously wrong in it. That is a finding.
- No file other than `planning_record.path` is written by this step.
- Nothing live is changed. A planning record is an internal record; publishing, CMS writes, and profile edits remain forbidden (policy kernel §1).
