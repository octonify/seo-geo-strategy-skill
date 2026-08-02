# Schema Type Decision

Owned by [`../SKILL.md`](../SKILL.md) step 10. Which structured-data type a page should carry, and — separately — what that type will and will not do.

---

## 1. Two questions, never merged

The single most common error in schema guidance is answering one question and reporting the other.

| Question | What it establishes | How it is answered |
|---|---|---|
| **A. Is this type a documented Google rich-result feature?** | Whether the markup can change how the result appears in Google Search | By reading Google's structured-data feature documentation, on a stated date |
| **B. Does this type help entity or answer-engine understanding?** | Whether it makes the page's subject machine-legible | By the type matching what the page actually is |

A type can be `no` on A and still worth recommending on B. A type that is `no` on A is **never** described as producing a rich result, an accordion, a snippet, or a SERP appearance of any kind.

`Done when` item 13 forces both answers into the output, with the date question A was checked:

```
| Page     | Type            | Documented rich result | Docs read on | Visible content it maps to |
|----------|-----------------|------------------------|--------------|----------------------------|
| <page-1> | <Type>          | yes                    | <YYYY-MM-DD> | <the visible content>      |
| <page-2> | <Type>          | no — entity value only | <YYYY-MM-DD> | <the visible content>      |
```

---

## 2. The documentation read

Google's list of structured-data features changes, and it has changed by removal more than by addition recently. So this file does not carry a frozen list as a rule. It carries the instruction to read the list and stamp the read.

**Procedure.** Open Google's structured-data feature gallery. For each type under consideration, record whether it appears. That read is `Measured` and carries its date. If the documentation cannot be read, the cell is `Unknown` — never `Estimated`. A feature is documented or it is not; a model's expectation of what Google supports is not evidence about what Google supports. (The same argument that made SERP composition `Measured`-or-`Unknown` in `docs/decisions.md` D13.)

### Dated snapshot — read 2026-08-02

Recorded as evidence of one read, not as a standing list. **Re-read it; do not cite this table as current.**

| Type | In the documented feature list on 2026-08-02 | Note |
|---|---|---|
| Article / BlogPosting | Yes | |
| Breadcrumb | Yes | |
| Local business | Yes | Knowledge-panel level detail: hours, ratings, directions |
| Organization | Yes | |
| Product, Review snippet, Merchant listing | Yes | Require genuine, visible, verifiable data |
| Video, Event, Recipe, Job posting, Course list | Yes | |
| Q&A, Profile page, Discussion forum, Speakable | Yes | Each with its own eligibility conditions |
| **FAQPage** | **No** | Deprecation notice dated 2026-05-07; FAQ rich results no longer appear. Still valid Schema.org |
| **Service** | **No** | Valid Schema.org, widely recommended in SEO writing, but not a documented Google rich-result feature. There is no "service snippet" |

**The two `No` rows are the reason this file exists.** Both are routinely presented in current practice as rich-result-earning types. Recommending either as such would put a promise into a brief that the SERP will not keep.

---

## 3. Choosing the type

Match the type to what the page **is**, then check question A.

| What the page is | Type that matches it | Then |
|---|---|---|
| An article, guide, or explainer | `Article` / `BlogPosting` | Check A |
| A page describing a service the business performs | `Service`, nested under the organisation | Check A — expect `no`; recommend on B |
| A page about the business itself, or a location | `LocalBusiness` (or its nearest subtype) | Check A. Coordinate with `local-presence-manager`, which owns the NAP values |
| A page whose visible content is a question-and-answer set | `FAQPage` | Check A — expect `no`; recommend on B only, and never promise an accordion |
| Any page with a parent in the cluster | `BreadcrumbList`, alongside the primary type | Check A |

Two rules constrain every row:

1. **The markup corresponds to visible content.** A type is recommended only when the brief actually requires the content it describes to be on the page. Marking up content that is not visible is a policy violation as well as a lie about the page.
2. **The brief states what the type will do.** Where question A is `no`, the brief's schema line says so in plain terms: this type aids machine understanding of what the page is; it produces no rich result.

### Where the CMS already emits a type

Read `site.seo_plugin` and `site.cms`. Where the declared plugin already emits a type for this page class, the decision is recorded as `already emitted by <site.seo_plugin> — confirm, do not duplicate`, and the finding is handed to the consuming project's implementation Skill. Two conflicting blocks of the same type on one page is a defect this Skill can predict and should not create.

Whether the emitted markup is actually present in the served page is an implementation question, not an architecture question. It is recorded as `Unknown` here and named as something the implementation Skill confirms.

---

## 4. Answer-engine value, stated honestly

Question B is worth answering, and it is also where unsupported claims cluster.

**What is well supported.** Current guidance converges on the page's clearest answer to its main question appearing near the top of the page, on heading hierarchy that reflects the actual structure of the content, and on sections that are self-contained enough to be read without their neighbours. Those are structural properties, they are decided here, and they go into the brief.

**What is contested, and is recorded as contested.** Whether deliberately fragmenting content into small units for machine extraction helps is disputed: Google's own guidance says writing for a human audience is sufficient and that multi-topic pages are understood, while independent GEO research reports measurable citation gains from more granular structuring. This file does not resolve that. The brief carries the well-supported items as requirements and records the contested one as a recorded disagreement, in the same way the pack records an intent disagreement rather than silently picking a winner.

**What is not encoded at all.** Citation-rate percentages, CTR uplift figures, and traffic-gain multipliers appear throughout current writing on this subject with no reproducible source behind them. None is written into a Skill file, a brief, or a record. Inventing a metric is forbidden by policy kernel §2, and quoting someone else's invented metric is the same act with an extra step.

---

## 5. What this file does not decide

- **The JSON-LD itself.** This Skill names the type and the visible content it must correspond to. Generating, placing, and validating markup is implementation, owned by the consuming project's implementation Skill.
- **Any property value.** Names, addresses, phone numbers, hours and ratings are values, and several of them are `local-presence-manager`'s to establish. This Skill never fills them.
- **Whether a rich result will actually appear.** Eligibility is not appearance. The brief says a page is eligible, never that a rich result is expected.
