# Design Decisions

Every non-obvious design decision, dated, with its reasoning and what would reverse it. A later session reads this instead of re-litigating settled questions.

Format: `## D<n> — <decision> — <date>`

---

## D1 — Build our own bundle rather than install the reference system — 2026-08-02

**Decision.** Take the architecture of `aaron-he-zhu/aaron-marketing-skills` (v19.1.0, studied at commit `46d6bc5`) as a design pattern, and author all content independently.

**Why.** Three reasons. The reference system is 16 SEO/GEO Skills inside a 120-Skill, seven-discipline bundle; most of it has no consumer in the current workflow. Its content layer would have to be overridden by a client voice Skill anyway. And a bundle we author can carry the domain knowledge already proven in production by the operator, which a generic bundle cannot.

**What we take.** The shared execution contract, evidence classification, decision gates, mechanically-checkable completion criteria, and the phase separation between research and decision.

**What we do not take.** Any file, schema, script, or text. The reference repository is Apache-2.0; influence is recorded in `LICENSE` and creates no obligation, but nothing is reproduced.

**Reverses if.** The reference system's methodology proves materially better than ours on a validation case we cannot match.

---

## D2 — Three Skills, split by completion criterion — 2026-08-02

**Decision.** `seo-geo-research`, `content-strategy-architect`, `local-presence-manager`.

**Why.** The split follows the rule that two things belong in different Skills when they have different completion criteria. Research is done when every candidate carries labelled metrics; architecture is done when every page has an owner and a boundary; local presence is done when one canonical NAP exists and the citation list has a status per source. These have no overlap in inputs or outputs.

The negative case is instructive: a sibling project's planning database mixed one-time intent data with continuously-changing state data under a single record with no write rule. The state fields rotted; the intent fields stayed clean. Mixing concerns with different lifecycles under one owner is the failure this split avoids.

**Reverses if.** In practice two of the three always run together with no meaningful decision point between them.

---

## D3 — Local presence in v1, not deferred — 2026-08-02

**Decision.** Include `local-presence-manager` in the first release.

**Why.** Operator instruction, supported by external evidence: Google Business Profile signals carry roughly a third of local pack ranking weight, making them the single strongest local factor. The existing manual workflow had no designed place for GBP at all — it appeared once, as post-publication follow-up. Encoding the workflow without it would have made that gap permanent.

**Evidence.** External search, 2026-08-02: local SEO guidance consistently ranks GBP signals as the dominant local-pack factor, and holds that a small number of strong service and location pages outperform unfocused blogging for local intent.

---

## D4 — Reject the event-sourced entity registry — 2026-08-02

**Decision.** Do not import the reference system's `protocol/entity-registry` component. Take only `page-play-builder/references/local.md` for local work.

**Why.** The entity registry is an append-only NDJSON event stream with owner-append semantics, multi-principal capability checks, projection rebuilds, and revision-conflict handling. It is built for reconciling machine-facing identity across a large organisation. Applied to a single-location clinic's NAP record, it adds substantial machinery and no benefit.

**What we take instead.** The canonical NAP record concept, the GBP checklist, the citation priority ordering, and the location/service-area page pattern — all of which are directly useful and carry no infrastructure requirement.

**Reverses if.** A consuming client has genuinely contested entity identity across many locations or brands.

---

## D5 — The bundle never writes copy — 2026-08-02

**Decision.** The handoff boundary is the content brief. A client-specific `{client}-content-voice` Skill writes all body copy. No generic writing Skill is included, now or later.

**Why.** Operator decision: every client gets its own voice Skill. Domain safety rules cannot be generalised — a naturopathic clinic's medical-claim constraints do not transfer to another industry, and a generic writer would either be useless or unsafe.

**Consequence.** Onboarding a new client requires building `{client}-content-voice` before this bundle can complete a chain. Recorded as a prerequisite in `README.md` and `architecture.md`.

---

## D6 — Proprietary licence — 2026-08-02

**Decision.** All rights reserved. Private repository.

**Why.** Operator decision. The bundle encodes client-facing methodology.

**Note.** `LICENSE` carries an attribution-of-influence section recording that the architectural approach was informed by an Apache-2.0 repository, while stating plainly that no source text is reproduced. This is a factual record, not a licence obligation.

---

## D7 — Repository named `seo-geo-strategy-skill`, singular — 2026-08-02

**Decision.** `github.com/octonify/seo-geo-strategy-skill`.

**Why.** Matches the operator's existing private Skill repository `wordpress-elementor-implementation-skill`, which is also singular despite containing multiple internal procedures. Internal consistency across the operator's own repositories outweighs consistency with the external reference naming.

"Strategy" rather than "content" marks the scope boundary in the name itself and leaves room for a sibling `seo-geo-implementation-skill` if the implement/tune phases are ever built.

---

## D8 — Evidence trail mandatory for primary-keyword selection — 2026-08-02

**Decision.** A primary-keyword recommendation is incomplete without a dated metric snapshot and a table of rejected alternatives with the reason each lost.

**Why.** Directly from a real finding. In a production project, two service pages were built. One recorded 204 screened candidates, seven validated phrases with dated local and national metrics, and an explicit multi-criteria rationale for the winner — reproducible. The other had a sound content architecture but no numeric snapshot survived, so the choice cannot be re-verified. The difference was not decision quality; it was whether the reasoning was captured.

**External validation.** 2026-08-02: industry guidance confirms the underlying method — classify by intent before selecting, verify against the actual SERP, and reject volume-only selection. A low-volume term with strong intent commonly outperforms a high-volume loosely-relevant one.

---

## D9 — Cluster-level volume aggregation added — 2026-08-02

**Decision.** Architecture must evaluate aggregate demand across a whole cluster, not only per-term volume.

**Why.** This appears in current external guidance on topic-cluster architecture and did **not** appear in the operator's existing manual method. It is an addition, not a codification of past practice — recorded explicitly so it is not mistaken for existing precedent.

**Evidence.** External search, 2026-08-02: evaluating aggregate cluster volume rather than isolated terms materially changes content prioritisation and reduces accidental cannibalization.

---

## D10 — Validation cases are real, not synthetic — 2026-08-02

**Decision.** Each Skill is validated against a known production case with a known answer.

| Skill | Case | Passing criterion |
|---|---|---|
| `seo-geo-research` | Gut Health keyword research | Independently reaches the same primary target, or a defensibly better one |
| `content-strategy-architect` | Hormone Health cluster | Flags the missing numeric snapshot as a defect without being told |
| `local-presence-manager` | Client NAP state | Independently finds the known site-vs-profile address mismatch |

**Why.** A Skill that only works on the example in its own documentation has not been tested. Each case has a known correct answer that the Skill was not shown.
