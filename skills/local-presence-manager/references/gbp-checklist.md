# Google Business Profile Checklist

Owned by [`../SKILL.md`](../SKILL.md), applied at step 5.

Thirteen items. Every one is recorded on every run, with a status, a date, and
how it was observed — including the items that are fine.

---

## 1. Read the guidelines, then stamp the read

Guideline compliance is checked against the documentation, read during the run,
with the date recorded in the record. It is never checked against recollection
and never against this file.

**Read on 2026-08-02**, from the platform's own guidelines for representing a
business:

| Rule | As documented |
|---|---|
| Name | The business's real-world name, as used on its storefront and stationery. Marketing taglines, store codes, trademark symbols, opening-hours text, phone numbers, URLs, and full capitalisation are outside it. Legal terms belong only where real-world signage carries them |
| Address | "Use a precise, accurate address and/or service area." P.O. boxes and mailboxes at remote locations are not acceptable. A business showing an address should maintain permanent fixed signage of its name at that address |
| Service-area business | A business that travels to customers "should hide your business address from customers" |
| Categories | "Use as few categories as possible to describe your overall core business", and choose categories "as specific as possible" |
| Hours | Provide regular customer-facing hours. Some venue types are documented as not needing them |

This snapshot is **evidence of one read on one date**, exactly as
`docs/decisions.md` D26 requires for schema eligibility. It is not a standing
list. The step re-reads; it does not cite this table as current.

Where the read cannot be performed on a run, every guideline-dependent item is
`Unknown — not checked`, and the record says the documentation was not read. It
does not fall back to this table.

## 2. The thirteen items

Status vocabulary, and nothing outside it: `present-correct`, `present-wrong`,
`missing`, `Unknown — not checked`.

| # | Item | `present-correct` when | `present-wrong` when | `missing` when |
|---|---|---|---|---|
| 1 | Profile identified | Exactly one profile is found for the location and its listing URL or place identifier is recorded | More than one profile is found for the location — record every one | A check was run and no profile was found |
| 2 | Verification state | The profile's own indicator shows it verified | The indicator shows unverified, suspended, or pending | The indicator is absent from the material observed |
| 3 | Name field | The published string matches the canonical name character for character, and carries nothing §1 places outside a name | It differs from the canonical, or carries a tagline, code, symbol, hours, number, URL, or full capitalisation | No name is published |
| 4 | Address, published or hidden | The address matches the canonical character for character; or the address is hidden and `service_area_mode` is `service_area` | The address differs from the canonical; or is published while the mode is `service_area`; or is hidden while the mode is `storefront`; or is a P.O. box or remote mailbox | No address and no service area is set at all |
| 5 | Service areas | Every area named in config or by the operator is present on the profile | The set on the profile differs from the set named — list both | The mode requires service areas and none are set |
| 6 | Primary category | One primary category is set, its exact string recorded, and it matches the category the operator or config named | Its string differs from the category named by the operator or config | No primary category is set |
| 7 | Additional categories | Each additional category's exact string is recorded | An additional category duplicates the primary, or names a service the business does not offer per the operator | — (none set is a valid state; record `present-correct` with count `0`) |
| 8 | Phone | The published number matches the canonical character for character | It differs from the canonical, including a call-tracking number where the canonical is a line number | No phone is published |
| 9 | Website URL | It resolves to `site.canonical_host` | It resolves to a different host, or to a redirect chain ending elsewhere — record both hosts | No website is set |
| 10 | Hours | Regular hours are set for every day the business states it is open, and any seasonal or holiday variation observed is recorded | Hours contradict the hours published on the site — quote both | No hours are set and §1 does not exempt this venue type |
| 11 | Description | A description is present, and its length is recorded | — see the boundary below | No description is present |
| 12 | Photos | At least one photo is present, and the count and the most recent date observed are recorded | A photo is observed to be stock or to depict a different business, per the operator | No photos are present |
| 13 | Services or products list | Entries are present and their count is recorded | An entry names a service on `constraints.retired_services` | No entries are present |

Every row also carries: the date observed, how it was observed (operator export,
dashboard screenshot, public listing, browser read), and its label from
[`observation-label-map.md`](observation-label-map.md) §1.

## 3. Two boundaries inside the checklist

**Presence is checked here. Wording is not.**

Item 11 records that a description exists and how long it is. It does not
evaluate the description, score it, suggest a phrase for it, or check whether a
keyword appears in its opening. Policy kernel §1 gives every wording decision to
the Skill named in `authority.authority_override_skill`, and a description is
wording end to end.

This is a deliberate departure from the source material, which instructs that
the primary keyword be placed within the first hundred characters of the
description. Two things are wrong with carrying that in. It is a wording
instruction, which this bundle does not issue. And the character threshold is an
unsourced figure of the kind `docs/decisions.md` D31 rejected — external
guidance read on 2026-08-02 holds that the description is not a direct ranking
input at all, contributing to profile completeness and to answer-engine
summaries rather than to position.

**Suitability is the operator's call, not the agent's.**

Item 6 marks a category `present-wrong` only when its string disagrees with a
category the operator or config named. Whether some other category would suit
the business better is a judgement about the business, and the Skill does not
make it. Where no category has been named by the operator, the observed string
is recorded and the item is `present-correct` on presence, with the unnamed
comparison listed in the Unknowns table.

External guidance read on 2026-08-02 is consistent that the primary category is
the single most influential profile field for local pack placement — which is
the reason the item is recorded exactly rather than summarised, and also the
reason a guess at a better one would be an expensive thing to be wrong about.

## 4. Deliberately not checked

Each with its reason. None of these is an oversight, and none is added without
the scope-expansion rule in `docs/architecture.md` §5.

| Not checked | Why |
|---|---|
| Reviews, ratings, review velocity | A continuously-changing state with its own lifecycle, which `docs/decisions.md` D2 keeps out of a record whose other fields are one-time decisions. External guidance read on 2026-08-02 places review signals second only to profile signals in local weight, so this is a real gap and is recorded as a proposal in the run report — not filled here |
| Replying to reviews | A live change to an external surface. Policy kernel §1 |
| Posts, offers, events, and their scheduling | Publication. Policy kernel §1, and a cadence, which `docs/architecture.md` §6 excludes |
| Questions and answers, messaging | Live interaction on an external surface. Policy kernel §1 |
| Performance insights, views, calls, direction requests | Post-publication measurement. `docs/architecture.md` §6 |
| Whether the profile is "optimised" as a score | No composite score appears anywhere in this bundle. `docs/decisions.md` D12 and D25 |
| Competitor profiles | A competitor's profile is not this unit. Competitor mapping from observed SERPs is `seo-geo-research`'s step 8 |

## 5. What a completed checklist is worth

Thirteen rows, each with a status, a date, and a method. That is the whole claim.

It is not a statement that the profile will rank, and the record makes no such
statement. External guidance read on 2026-08-02 attributes roughly a third of
local pack weight to profile signals in aggregate — which is why the checklist
exists and why every item is recorded rather than sampled. It is a distribution
reported by third parties about a system nobody here can observe, it is carried
as context in `docs/decisions.md` D3, and it is not arithmetic anyone should do
against an individual profile.
