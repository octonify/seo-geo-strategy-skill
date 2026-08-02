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

---

## D11 — Research produces evidence and names no target — 2026-08-03

**Decision.** `seo-geo-research` outputs a labelled evidence pack. It selects nothing, ranks nothing, and sequences nothing. `Done when` item 11 enforces this mechanically: the pack may contain no column headed `Priority`, `Score`, `Tier`, `Rank`, or `Quick win`, and no section headed `Recommendation`, `Primary keyword`, `Cluster`, `Content calendar`, or `Next steps`.

**What we take.** The reference system's separation of a survey phase from a decision phase (D1, already settled).

**What we reject, having read it.** The reference `keyword-research` Skill's delivery sections — Executive Summary, Quick Wins / Growth / GEO opportunities, Topic Clusters, Content Calendar, Next Steps — and its `Opportunity = (Volume × Intent Value) / Difficulty` formula with intent values 1/1/2/3.

**Why reject.** Both name a target from inside the research Skill. The reference system's research Skill recommends what to write, which collapses `architecture.md` §2's boundary: research is done when every candidate carries labelled metrics; architecture is done when every page has an owner and a boundary. A Skill that does both has neither completion criterion.

**Reverses if.** A consuming project runs research without ever running architecture, making the evidence pack a dead end in practice.

---

## D12 — Reject every composite priority score — 2026-08-03

**Decision.** No weighted composite score appears anywhere in this Skill. Difficulty is read as a set of separately-labelled inputs (`serp-read-protocol.md` §6), never as one number of our own construction.

**What we reject, having read it.** Four scoring models from packages 06, 07 and 11: the Priority Score matrix (volume 20% / difficulty 25% / relevance 30% / intent 15% / trend 10%, bucketed P0–P3); the Opportunity Score; the Impact × Confidence lens with BOFU/MOFU/TOFU tagging; and the Gap Priority Score with its Quick Win arithmetic.

**Why reject.** Two independent reasons, either sufficient.

First, a composite cannot carry an honest evidence label. Its inputs are a mix of `Measured`, `Estimated` and `Unknown`. Policy kernel §2 forbids presenting an estimate as measured, and a single number derived from that mix has no label that is true of it. Worse, `Unknown` inputs must be given *some* value for the arithmetic to complete — which is exactly the "`Unknown` silently becomes zero or a default" failure the kernel names.

Second, a score exists to rank candidates against each other, and ranking candidates is the decision D11 places in `content-strategy-architect`.

**What we keep instead.** Every input stated separately with its own label, plus one sentence describing what the inputs jointly show about the SERP. A reader can build any weighting they want; they cannot be handed one silently.

**Reverses if.** Architecture proves unable to decide without a pre-computed rank, across more than one real case.

---

## D13 — SERP composition is `Measured` or `Unknown`, never `Estimated` — 2026-08-03

**Decision.** A SERP was observed or it was not. A model's expectation of what a SERP probably contains is not evidence about what it contains, and this Skill has no label for it.

This is **stricter than policy kernel §2**, which permits `Estimated` for model inference generally. It narrows the permitted set for one class of metric; it adds no label and contradicts nothing.

**Why.** The observed-difficulty read is built on top of composition. An inferred composition would silently become an inferred difficulty, and a downstream Skill reading the pack would have no way to tell the difference. The same argument does not apply to a volume, where the tool name and date make the provenance visible in the value itself.

**This is an addition, not codified past practice.** The archived Gut Health research recorded SERP screenshots as evidence but had no rule preventing an unobserved SERP from being described. Flagged per the D9 pattern so it is not mistaken for precedent.

**External validation.** Search, 2026-08-03: current guidance treats tool difficulty scores as estimates that vary substantially between tools and holds that manual SERP inspection is required to catch what a score misses — a high-difficulty query whose top ten is thin, outdated, or directory-filled. That is an argument for observation over inference, which is what this rule makes non-optional.

---

## D14 — A tool-reported zero is `Unknown`, never a demand figure — 2026-08-03

**Decision.** When a keyword tool reports local volume as `0`, the pack records `Unknown — tool reports 0 for <locality>` and carries the national figure on the same row. Both lines always appear together. `Done when` item 5 enforces it: no volume cell may contain `0`.

A population-ratio figure (`national × locality population ÷ dataset population`) is permitted only as `Calculated`, only with both population inputs themselves labelled, and never in place of the `Unknown` line.

**Why.** A tool reporting zero for a locality is reporting that it has no data for that locality, not that nobody searches the term. Policy kernel §2 already forbids `Unknown` silently becoming zero; this decision names the specific mechanism by which it was happening.

**Evidence from the validation case.** The archived Gut Health keyword list holds 204 rows, of which 58 carry a blank volume and 8 carry `0`. Among them, `naturopathic doctor for gut health` is recorded as volume `0`, difficulty `0`, intent blank — and was rejected for "insufficient demand". Its locality-set SERP is populated, carries a local pack, and returns three comparable local providers in its top three. Zero data and zero demand were treated as the same fact.

**External validation.** Search, 2026-08-03: geo-modified queries in smaller markets routinely return zero from tools that carry real national volume for the same phrase, because the tool lacks per-city coverage rather than because demand is absent. The population-ratio derivation is the commonly-cited workaround, and is treated in that guidance as an estimate — which is why it is admitted here only as a labelled `Calculated` value beside the `Unknown`, not instead of it.

---

## D15 — Intent is classified twice, and the SERP wins — 2026-08-03

**Decision.** Every candidate carries two intent classifications: Pass A from the query pattern (`Estimated`, always) and Pass B from the observed SERP (`Measured` or `Unknown`, never `Estimated`). Where they disagree, Pass B is authoritative and **both are kept**, with the disagreement recorded as a finding.

**Why the disagreement is kept rather than resolved.** Directly from `skill-contract.md` §4's corollary: validating an output against an authority that can itself be wrong is not validation, and where a check compares two records, the file must state which wins. A tool's intent label is a model's opinion about a query; the SERP is the engine's decision about it. Recording only the winner destroys the finding.

**Evidence from the validation case.** `gut health doctor` returns intent `Informational` at the US dataset and `Navigational` at Kirkland, WA — the same string, the same tool, the same day. The cause is visible only in the SERP: one brand entity whose name is the query holds positions 1 (with sitelinks), 2 (its Instagram profile) and 3. A single-value intent column would have recorded one of those two labels and lost the reason for both.

**Sub-intent is an addition, flagged.** The four-class scheme is too coarse to imply a page format. A seven-value sub-intent layer (definitional, instructional, diagnostic, comparative, reassurance, provider-seeking, access) is attached and marked as an addition wherever it appears. **External validation.** Search, 2026-08-03: current guidance holds that the traditional four-intent classification is no longer granular enough and that narrower sub-intents each call for a different content format, with SERP-feature presence the most reliable secondary signal for refining the classification.

**Boundary.** Sub-intent names a format. It never names the wording. What a reassurance-intent query should be answered *with* is decided by the Skill in `authority.authority_override_skill`.

---

## D16 — Search Console query mining is a discovery source, not rank tracking — 2026-08-03

**Decision.** `seo-geo-research` may read a Search Console query export once, for the current run, as discovery source 2. It records position as an observed value at the export date. It does not establish a cadence, compare against a prior run, or report movement.

**Why this needed deciding.** `architecture.md` §6 excludes rank tracking and performance monitoring from the bundle, and a query export contains positions. The distinction drawn here is between *demand discovery* — which terms this site already receives impressions for, read once — and *position monitoring over time*, which is a separate lifecycle with a separate cadence and is the thing §6 excludes. First-party impression data is the only `Measured` demand source available to a project with no paid tool, and excluding it would have made the zero-tool path materially weaker for no gain.

**Boundary made explicit.** `keyword-universe-sources.md` §1 states the rule in the reference itself, and states that a request for movement is a different request on which this Skill stops rather than widening.

**Flagged for the coordinating agent.** This is a boundary interpretation, not a scope expansion, but it is close enough to the §6 line to be worth confirming rather than assuming.

---

## D17 — Research reads and writes no planning record — 2026-08-03

**Decision.** `seo-geo-research` does not read `planning_record.path`, `planning_record.owned_fields`, or `planning_record.row_identifier_field`, and writes no planning row.

**Why.** Policy kernel §6 governs writes into a consuming project's records and requires, among other things, that a target row be identifiable unambiguously. A research pack has no row to identify — the planning row belongs to a *page*, and a page does not exist until architecture decides one should. Giving research write access to the planning database would recreate exactly the failure D2 was drawn to avoid: two lifecycles sharing one record with no write rule.

**Consequence.** The evidence pack is the entire handoff. Architecture reads it and writes the planning row.

---

## D18 — No config key for the research output path; the operator supplies it — 2026-08-03

**Decision.** The pack is always emitted in session. A file is written only to a directory the operator supplies at run time, as `<dir>/<client.id>-<topic-slug>-keyword-evidence-<YYYY-MM-DD>.md`. No directory is assumed and no path is invented.

**Why.** `project-config.schema.yaml` defines no key for a research output directory, and that file is shared-layer foundation this task was not authorised to edit. Inventing a path would violate `skill-contract.md` §6; adding a required key would edit the foundation; making it a *required* runtime input would block a Skill that has a perfectly good in-session output.

**Recorded as a proposal, not implemented.** An optional `research_output.path` key would remove the run-time question. It is not added here. See the run report for 2026-08-03.

---

## D19 — Skill files carry `version: 0.0.0-unreleased` until the first tag — 2026-08-03

**Decision.** Every `SKILL.md` in this bundle carries `version: 0.0.0-unreleased` in frontmatter until a release is cut.

**Why.** `skill-contract.md` §2 requires a bundle version in frontmatter and §8 requires that all Skills share one. No tag exists: `VERSIONS.md` states that none will be cut until all three Skills pass their D10 validation case. Writing `1.0.0` into a file that is not in a 1.0.0 release would make the field a claim rather than a fact, and installed copies are supposed to be byte-identical to a tag.

**Consequence.** Cutting the first release is a mechanical find-and-replace across three files, plus the `VERSIONS.md` entry with its stated reason.

---

## D20 — Source package cherry-pick ledger, packages 06–11 — 2026-08-03

Every candidate file read before the accept/reject call. Apache-2.0 source; **no text reproduced from any of them**, per D1.

| Package / file | Verdict | Basis |
|---|---|---|
| 06 `keyword-research/SKILL.md` | **Reject** as a whole | Recommends targets from inside research — see D11 |
| 06 `references/instructions-detail.md` — 8-phase workflow | Partial accept | Phase *sequence* (scope → discover → expand → classify → cluster) is sound; the score and deliver phases are rejected per D11/D12 |
| 06 `references/instructions-detail.md` — modifier patterns | **Accept**, rewritten | Useful phrasing generator. Re-authored around provider-and-place patterns, which the source's SaaS-shaped list omits and a local service unit needs most |
| 06 `references/keyword-intent-taxonomy.md` — four-class matrix | **Accept**, rewritten and extended | Sound core; extended with the sub-intent layer and the dual-pass rule per D15 |
| 06 `references/keyword-intent-taxonomy.md` — funnel mapping with conversion-rate bands | **Reject** | Quotes conversion percentages per funnel stage with no source. Inventing a metric is forbidden by policy kernel §2 |
| 06 `references/topic-cluster-templates.md` | **Reject** for this Skill | Cluster design is `content-strategy-architect`'s unit |
| 06 `references/example-report.md` | **Reject** | Worked example of the rejected delivery format |
| 07 `keyword-prioritization-framework.md` | **Reject** | Composite scoring — see D12 |
| 07 `gap-analysis-frameworks.md` — segment map (only you / shared / only them / no one) | **Accept**, rewritten | Genuinely useful. Re-authored as Held / Contested / Uncovered / Open / Unknown, each bound to an observed ranking URL and each carrying its own label |
| 07 `gap-analysis-frameworks.md` — Opportunity Score, Quick Win arithmetic, calendar integration | **Reject** | Composite scoring and sequencing — D11, D12 |
| 08 `serp-analysis/SKILL.md` | Partial accept | The step order (composition → top pages → patterns → features → intent → difficulty) is sound and is the basis of `serp-read-protocol.md`. The single 0–100 difficulty output is rejected per D12 |
| 08 `references/serp-feature-taxonomy.md` | **Accept** as a checklist source, rewritten | The feature inventory is comprehensive and worth having as a ten-item check. Its optimisation advice ("win by structure", "citation drivers") is rejected — that is implementation and language, owned elsewhere |
| 08/09 `references/analysis-templates.md` — capture fields | **Accept**, rewritten | Position / URL / domain / authority / freshness / links is the right per-result capture set. Extended with the result-type taxonomy, which is the field carrying the signal a difficulty number cannot |
| 09 True Difficulty — weighted 0–100 (authority 25%, page links 20%, content bar 20%, backlinks 20%, stability 15%) | **Reject** | The most considered scoring model in the source set, and still rejected: it produces one unlabellable number from mixed-quality inputs — D12. Its five *input categories* are accepted as separately-labelled rows |
| 09 Site-stage fit (new / growing / established) | **Reject** | A recommendation about who should target the term |
| 10 `competitor-analysis/SKILL.md` — decision gates | **Accept** as a pattern | The stop-and-ask / continue-silently split with a stated default is the shape used here. Its content is re-derived for this unit |
| 10 `competitor-analysis` — backlink profile, technical SEO, Core Web Vitals steps | **Reject** | Explicitly out of scope, `architecture.md` §6 |
| 10 `references/analysis-templates.md` — competitor profile fields | **Accept**, rewritten | Re-authored around observed SERP appearances rather than asserted rivalry, and stripped of the qualitative "strengths / weaknesses" columns, which are judgements |
| 10 `references/battlecard-template.md`, `positioning-frameworks.md` | **Reject** — not read past their purpose | Sales positioning artifacts, no consumer in this workflow |
| 11 `content-gap-analysis/SKILL.md` | Partial accept | Gap-must-name-the-competitor is the right rule and is tightened here to gap-must-name-the-URL. Prioritisation and calendar output rejected per D11 |
| 11 `references/analysis-templates.md`, `example-report.md` | **Reject** | Templates for the rejected output shape |

**Note on the source's own strengths.** Three things in the source set are better than a first reading suggests and were adopted deliberately: the insistence that every claim cite a specific number, the explicit treatment of retrieved content as untrusted, and the "generic vs actionable" contrast that makes a quality bar checkable. All three are already present in this bundle's shared layer, independently arrived at.
