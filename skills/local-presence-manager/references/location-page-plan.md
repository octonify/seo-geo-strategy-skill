# Location And Service-Area Page Plan

Owned by [`../SKILL.md`](../SKILL.md), applied at step 7.

The plan says **which pages exist and what each must carry**. It does not say
what any of them ranks for, and it does not say what any of them says.

---

## 1. The pattern comes from the mode

`local_presence.service_area_mode` decides it. The record states which mode
produced the pattern, so a reader can see the plan follow from a config value
rather than from a preference.

| Mode | Pages | Each page carries | Each page does not carry |
|---|---|---|---|
| `storefront` | One page per physical location | The canonical NAP as visible text · an embedded map of the location · one owning locality | — |
| `service_area` | One page per service area named by the operator or config | The canonical NAP **name and phone** as visible text · the defined service area stated · one owning locality | **No published street address and no embedded map.** The guideline read in [`gbp-checklist.md`](gbp-checklist.md) §1 states a service-area business should hide its address, and a page publishing what the profile hides reintroduces the inconsistency the canonical exists to prevent |
| `hybrid` | Both patterns, side by side | Per the pattern each page belongs to | Per the pattern each page belongs to |

Under `hybrid` the two patterns are produced separately and the record states
which locality each page owns. They are never collapsed into one pattern,
because the address rule differs between them and collapsing decides it by
accident.

## 2. One locality, one page

Every page owns exactly one locality, and no locality appears on two rows.

This is the same rule `content-strategy-architect` applies to terms
(`Done when` item 11 there), applied to places. Two pages for one locality
compete with each other for every query naming it, and the cheapest moment to
prevent that is before either exists.

Where an operator names two areas that are the same place under two names, the
Skill records both names against one row and states the pair. It does not decide
that they are the same place from the names alone.

## 3. What a page must carry, and who decides the rest

| Element | Decided here | Decided elsewhere |
|---|---|---|
| The canonical NAP appears as visible text | Yes — which fields, per the mode | The wording around it: the voice Skill |
| One owning locality | Yes | — |
| Embedded map, or its absence | Yes, from the mode | — |
| Service area stated | Yes, from config or the operator | How it is phrased: the voice Skill |
| Which term the page owns | No | `content-strategy-architect`, from an evidence pack |
| Cluster role, boundary sentence, internal links | No | `content-strategy-architect` |
| Schema type and its rich-result eligibility | No | `content-strategy-architect`, per its `schema-decision.md` and `docs/decisions.md` D26 |
| Title tag, headings, body copy, calls to action | No | The Skill in `authority.authority_override_skill` |
| Page template, layout, imagery | No | The consuming project's design and implementation Skills |

The Page Plan is handed to `content-strategy-architect` as an input: a list of
pages that must exist for local reasons, each with its locality and its
disposition. That Skill decides what each one targets and how it links, and it
may hold or re-scope a page on evidence this Skill does not carry. **The plan
proposes pages; it does not reserve them.**

## 4. Disposition

One per row, from the inventory of what already exists on `site.canonical_host`.

| Disposition | When |
|---|---|
| `keep` | A page for this locality exists, carries the canonical NAP correctly, and needs nothing |
| `extend` | A page for this locality exists and is missing a required element, or carries a NAP variance |
| `create` | No page for this locality exists |
| `retire` | A page exists for a locality no longer served, or a second page exists for a locality another page already owns |

`retire` is a recommendation like any other. Nothing is unpublished, redirected,
or removed by this Skill — a redirect is a live change and is outside this
bundle entirely (`docs/architecture.md` §6, and `docs/decisions.md` D32 rejected
the source material's migration safeguards for the same reason).

Where a page's existence could not be confirmed either way, the disposition is
`Unknown` and the row says what would resolve it. It is never `create` by
default: creating a duplicate of a page nobody looked for is the expensive error,
and the asymmetry is the same one `docs/decisions.md` D28 fixed for clusters.

## 5. The duplication constraint

Each page is about its own locality. A set of pages differing only in the place
name is a set of doorway pages.

External guidance read on 2026-08-02 is consistent that near-duplicate
location-page sets are treated as scaled content abuse and can be deindexed as a
set, and that this enforcement has tightened rather than relaxed. That is the
constraint. What is **not** carried in from that guidance is every number
attached to it — a percentage of shared content at which detection fires, a
proportion of a page that must be unique, a number of pages per week, a count of
cities worth targeting. Each is an unsourced threshold, and policy kernel §2
forbids inventing a metric or repeating an invented one.

So the constraint is stated in the plan as a requirement on each page, and the
requirement is **not** met by anything this Skill produces:

> Each page's content is specific to its locality. Producing that content is the
> job of the Skill named in `authority.authority_override_skill`.

A page plan that hands over a boilerplate the voice Skill is expected to
find-and-replace has built the doorway set itself, one step earlier. So no
boilerplate is produced here — not as a template, not as an example, not as a
starting point.

## 6. Page count is not sequenced here

The plan names the pages. It does not order them, phase them, batch them, or say
which is written first.

Sequencing is a decision this bundle does not make — `docs/decisions.md` D11 for
research, D27's boundary for architecture, and the same line here. Where the
operator asks which locality to start with, the Skill hands over what it
observed — which localities have an existing page, which have a NAP variance,
and, if a `seo-geo-research` pack was supplied, which terms its GEO surfaces
table observed a local pack for — and stops there.
