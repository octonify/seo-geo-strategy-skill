# Canonical NAP Record

Owned by [`../SKILL.md`](../SKILL.md), applied at steps 3 and 4.

The canonical NAP is **one exact string per field, agreed once**. Everything
else in this Skill compares against it. Get it wrong and every listing built on
it is wrong in the same way.

---

## 1. The record

Three fields. One value each. No alternates, no "or", no parenthesised variant.

| Field | What it holds | Origin | Label |
|---|---|---|---|
| Name | The business name as one exact string | `local_presence.canonical_nap.name`, or an observed source named under gate 2 option 2 | `User-provided` or `Measured` |
| Address | The address as one exact string, in one format | `local_presence.canonical_nap.address`, or as above | `User-provided` or `Measured` |
| Phone | One number, in one format | `local_presence.canonical_nap.phone`, or as above | `User-provided` or `Measured` |

A field with two acceptable forms is not agreed. Write it as `Unknown — not
agreed` and take gate 2 or gate 4 rather than carrying an ambiguity forward into
every comparison.

## 2. The format choices that have to be decided

Each of these is a decision, not a variant. The record names the chosen form and
the Format Decisions table names what else was observed.

| Choice | Forms seen in practice | Decided by |
|---|---|---|
| Suite designator | `Suite` · `Ste` · `Ste.` · `Unit` · `#` · omitted entirely | Operator or config. Never by the agent |
| Street type | `Street` · `St` · `St.`, and the same for Avenue, Road, Boulevard | Operator or config |
| Directional | `NE` · `N.E.` · `Northeast`, and its position before or after the street name | Operator or config |
| Ordering of the secondary unit | before the street line, after it, or on its own line | Operator or config |
| Legal suffix in the name | `LLC` · `Inc.` · omitted | Operator or config, and see §6 |
| Trailing descriptors in the name | included · omitted | Operator or config, and see §6 |
| Phone punctuation | `(NNN) NNN-NNNN` · `NNN-NNN-NNNN` · `+1 NNN NNN NNNN` · digits only | Operator or config |
| Locality and region form | full state or province name versus its abbreviation | Operator or config |

**The agent decides none of these.** It observes which forms exist, names the
contest, and takes the gate. An agent that picks the form appearing most often
has invented a canonical from a headcount, and a count of directories is not
evidence about a business's own name.

## 3. Where the canonical comes from

In this order, and no further:

1. **`local_presence.canonical_nap`**, when all three fields are present. Label
   `User-provided`, origin the config key.
2. **One named observed source**, adopted by the operator under stop-and-ask
   gate 2 option 2. Label `Measured`, origin that source with its date. The
   record names which source, so a later run can see what the canonical was
   built on.
3. **Nothing.** The run is observation-only, all three fields read
   `Unknown — not agreed`, and Status is `partial`.

There is no fourth source. The agent never derives a canonical from the
observations by majority, by recency, by domain authority, or by which string
looks most complete.

## 4. The comparison

Character for character, per field, against every row of the Observed Sources
table.

**The comparison runs whether or not a canonical was agreed.** Where none was,
the base is the first Observed Sources row — the site's primary NAP surface —
and the variance table says so at its head:

```
Comparison base: <source>, observed <YYYY-MM-DD>.
This is a base for comparison, not a canonical. No canonical was agreed.
```

The site is the base because it is the surface the business most directly
controls and the one it can change without a third party's approval. That is a
reason to compare *from* it. It is not a claim that it is correct, and the
variance rows are read as "these two disagree", never as "that source is wrong".

Deferring the comparison until a canonical exists would make the disagreement
invisible in exactly the case where the presence has never been audited — which
is the case the audit is for.

Compare the strings **as transcribed**. Do not lowercase, strip punctuation,
expand abbreviations, or reorder components before comparing — those
transformations are exactly the differences being looked for.

Every difference is one row of the NAP Variance table, quoting both strings in
full. A row that says a source "differs slightly" without quoting the strings is
not a finding; it is a note that a finding was seen and not written down.

## 5. Classifying a difference

Three classes. Every variance row carries exactly one.

| Class | Means | Example shape |
|---|---|---|
| `digits-differ` | The digits of the phone, the street number, or the postal code are not identical | A transposed street number; a different phone line entirely |
| `words-differ` | A word is present on one side and absent or different on the other, beyond formatting | A missing secondary-unit line; a different street name; a name field carrying a descriptor the canonical does not |
| `format-only` | The same words and digits, differently written | `Suite` against `Ste`; `(NNN) NNN-NNNN` against `NNN.NNN.NNNN` |

Every `format-only` row states what is identical underneath it, so a reader can
see that the classification was made by comparison rather than by impression.

**No class is dismissed as harmless.** External guidance is split on
consequence: format differences in a secondary unit are widely reported to have
little effect on how the engine resolves one business from another, while the
same guidance holds that inconsistent strings across a business's own surfaces
erode trust in the record and can place a map pin wrongly. Both halves of that
are hearsay about a system nobody here can observe. What is observable is that
the strings disagree, and that is what the record states.

## 6. The name field has a rule the other two do not

The address and phone are facts about a place. The name is partly a fact and
partly a claim, and the platform publishing it constrains what it may contain.

Read against the guideline documentation at the date stated in
[`gbp-checklist.md`](gbp-checklist.md) §1, a profile name is the business's
real-world name as used on its signage and stationery. Marketing taglines, store
codes, trademark symbols, opening hours, phone numbers, URLs, and full
capitalisation are outside that. A legal suffix belongs only where the
real-world signage carries it.

Therefore:

- A name field carrying more than the real-world name is a **guideline finding**,
  recorded as `present-wrong` on the GBP checklist with the observed string
  quoted, and given a Remediation row.
- It is **not** rewritten here. What the name should say, where a choice exists,
  is language, and policy kernel §1 gives language to the Skill named in
  `authority.authority_override_skill`. This file names the constraint; that
  Skill writes within it.

## 7. Site versus profile is a finding either way

The live site and the Google Business Profile are both the business's own
statements about itself. When they disagree, the disagreement is the finding —
independent of which one the canonical happens to follow, and independent of how
small the difference looks.

This is stated explicitly because the tempting move is to resolve it: pick the
canonical, mark the other side `present-wrong`, and move on with one tidy row.
That records the correction and loses the fact that two first-party surfaces had
drifted apart, which is the thing worth knowing about how the presence is
maintained.

So both are recorded: the variance row, and a line in the record naming it as a
first-party disagreement rather than a third-party staleness.

**This is an addition, not codified past practice.** The source material this
Skill drew on audits the profile and each directory and does not read the
website as a NAP source at all. Flagged per the `docs/decisions.md` D9 pattern so
it is not mistaken for existing practice.
