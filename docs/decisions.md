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

---

## D21 — Confirm D16, with the boundary tightened — 2026-08-03

**Decision.** A Search Console query export is admitted as a discovery source. The line against the `architecture.md` §6 exclusion is drawn at the **operation**, not the data source.

Permitted: a one-time read of which queries already produce impressions, used as `Measured` demand evidence at a point in time.

Forbidden, and this is what §6 excludes: retaining exports for period-over-period comparison, analysing position change, any "was 12, now 8" framing, or any scheduled re-read. A Skill that finds itself comparing two exports has left this bundle's scope.

**Why.** The exclusion in §6 targets ongoing position monitoring — a different lifecycle, a different cadence, and a different consumer. One-time demand discovery is neither. Practically, first-party impression data is the only `Measured` demand signal available to a project with no paid tool; removing it would leave the zero-tool path with no measured demand at all, and §6 was never intended to have that effect.

**Reverses if.** A consuming project acquires a rank-tracking capability whose owner should hold this data instead.

---

## D22 — Add `research_output.path` to the schema as optional — 2026-08-03

**Decision.** Approve the D18 proposal. `project-config.schema.yaml` gains an optional `research_output.path`. Coordinating-agent authority; D18 correctly declined to self-authorise a shared-layer edit.

**Why.** Not a scope expansion. The Skills already write a file when given a destination; this only removes a run-time question. Optional, so the in-session default and the never-invent-a-path rule are unchanged.

---

## D23 — `Calculated` added to the handoff evidence-basis line — 2026-08-03

**Decision.** `skill-contract.md` §5 now enumerates all five labels. The local convention of folding `Calculated` under its weakest input label is withdrawn.

**Why.** A defect in the shared layer, introduced when it was authored: the policy kernel defines five evidence labels and the handoff block enumerated four. Three Skills would each have invented a local workaround for the same inconsistency. Fixed once, centrally.

**Consequence.** `seo-geo-research` should drop its folding convention and count `Calculated` directly. Carried as a follow-up.

---

## D24 — Architecture decides link targets; it never decides anchor wording — 2026-08-02

**Decision.** The internal link map carries a **target concept** — what the link is about — and never an anchor phrase. `references/internal-link-map.md` §4 draws the line, and the record carries no column headed `Anchor text` or `Suggested anchor`.

**Why this needed deciding.** Anchor text sits exactly on the seam. That a link should describe where it goes is a property of the link graph and belongs here. The words that do the describing are language and belong to the Skill in `authority.authority_override_skill` (policy kernel §1). Every internal-linking source read for this Skill hands over suggested anchors, and each one reads as helpful rather than as a boundary crossing — which is precisely why the rule has to be written down rather than left to judgement.

**What we reject, having read it.** Package 27's Step 5 contextual-link template, whose columns are source paragraph, target URL, **suggested anchor**, priority; and its anchor-text distribution targets (descriptive 60–80%, branded 10–20%, generic under 10%, exact-match under 5% per target).

**Why reject the distribution targets specifically.** They are unsourced percentages presented as thresholds, and they are thresholds *about wording*. Both halves fail: policy kernel §2 forbids inventing a metric, and policy kernel §1 gives the wording to another Skill.

**Reverses if.** A consuming project's voice Skill declines to own anchor wording, leaving it unowned.

---

## D25 — Reject the structure score, as D12 rejected the keyword score — 2026-08-02

**Decision.** No architecture score, no structure score, no /100 of any kind appears in this Skill.

**What we reject, having read it.** Package 26's architecture score (start 100; −10 per orphan, −10 per island, −5 per important page deeper than three clicks, −10 per URL migration without a planned 301, −5 per inconsistent URL parent), its linking-mode structure score, and package 27's Anchor Score /10.

**Why.** `docs/decisions.md` D12's reasoning transfers unchanged: a composite over inputs of mixed evidence quality carries no label that is true of it, and completing the arithmetic requires giving `Unknown` inputs a number. The scores here are worse than the keyword scores in one respect — their penalty weights are stated to the point, with no source, which makes an invented metric look like a measurement.

**What we keep instead.** The required links are checked and reported as counts of what is present against what is required (`Done when` item 12). A reader can see the gap without being handed a number that hides which part of it matters.

---

## D26 — The schema decision separates rich-result eligibility from entity value, and `FAQPage` and `Service` are both `no` — 2026-08-02

**Decision.** Every recommended schema type is assessed on two questions that are never merged: is it a documented Google rich-result feature, and does it aid entity or answer-engine understanding? The first is answered by reading Google's feature documentation and stamping the read with its date. It is `Measured` or `Unknown`, never `Estimated`.

**Evidence.** Google's structured-data feature gallery, read 2026-08-02: 30 documented features. `LocalBusiness` is among them. **`Service` is not.** **`FAQPage` is not** — external search the same day confirms a deprecation notice dated 2026-05-07, after which FAQ rich results no longer appear for any site, including the government and health verticals that had retained eligibility after the August 2023 restriction.

**What we reject, having read it.** Package 18's content-to-schema table, which maps a service page to `Service` schema with the rich-result eligibility "Service snippet". There is no such Google rich result. The same table lists `FAQPage` producing an "FAQ accordion in SERP", which was true when written and is not now.

**Why this matters more than a corrected row.** A brief that says a page is eligible for a rich result makes a promise the SERP either keeps or does not. Encoding a type as rich-result-earning when it is not puts an unkeepable promise into every brief that uses it, and nothing downstream is positioned to catch it.

**This is an addition, flagged.** The operator's existing practice has no rule separating the two questions, and the planning record in the validation case declares `FAQPage` on five rows. Flagged per the D9 pattern so it is not mistaken for precedent.

**Consequence.** The dated snapshot in `schema-decision.md` §2 is recorded as evidence of one read, explicitly not as a standing list, and the Skill re-reads rather than citing it.

**Reverses if.** Google restores FAQ rich results, or documents `Service` as a feature. Both are re-checked by the step itself, which is the point of stamping the read.

---

## D27 — Aggregate cluster demand is reported as a floor, never as a total — 2026-08-02

**Decision.** D9 requires evaluating demand across the whole cluster. The aggregate is reported as a **floor** over the members whose demand is known, plus the named list of members whose demand is `Unknown`. Where every member is `Unknown` there is no floor and the line reads `Unknown`. `Done when` item 6 checks that the word `floor` appears whenever any member is `Unknown`.

**Why.** D9 as written does not survive contact with a partial pack. Summing demand across members requires a number for every member, and an `Unknown` member has none — supplying one is the "`Unknown` silently becomes zero" failure policy kernel §2 names, arriving through arithmetic rather than through carelessness. A floor is the strongest statement the evidence actually supports, and it stays honest at every level of pack completeness.

**Boundary.** The aggregate sizes the proposition and feeds the brief's context. It never ranks this cluster against another and never sequences which page is written first. Sequencing is not this bundle's decision, and a cross-cluster comparison built on floors of differing completeness would be a composite score by another name — D12.

---

## D28 — One page or two is decided by observed SERP overlap, and an unobserved pair is never split — 2026-08-02

**Decision.** Two candidate terms share one page when their observed top tens have **4 or more URLs in common**; 3 or fewer means separate pages. The threshold is stated as a sentence in the record every run. Where either SERP was not observed, the pair is `Unknown` and is **not** split; the second term is held.

**Why a threshold at all.** "Do these two terms need two pages?" is otherwise answered by how different the phrases look, which is the intuition that builds cannibalization deliberately. The overlap count answers it from what the engine actually returned.

**Why 4, and why it is stated openly.** External validation, 2026-08-02: published practice puts the useful band at roughly 3–6 shared URLs of the top ten, with 4 the common middle. It is a convention, not a measurement, so the record states which number was used rather than applying it invisibly. An operator who wants tighter or looser clusters changes it, and the change is visible.

**Why the unobserved default is "one page".** The asymmetry is not obvious and is therefore fixed here. Splitting wrongly creates two live pages that compete, and unwinding that is expensive. Not splitting wrongly leaves a page unbuilt, which costs nothing that was not going to be spent anyway. **Absent evidence never authorises a new page.**

**This is an addition, flagged.** The validation case's planning record contains the same instinct written as prose — several rows say a separate post should not be published "unless SERP proves separate intent" — but with no test, no threshold, and no record of the test ever having been run. Encoding the test is the addition.

---

## D29 — Re-verification of inherited decisions runs before the evidence pack is required — 2026-08-02

**Decision.** The inventory of existing pages and the re-verification of their decisions is step 2, ahead of pack ingestion at step 3, and it runs on every run. Stop-and-ask gate 3 (no pack) gained a third option: a **re-verification-only run** that emits the inventory, the defects and the unknowns, marks `Done when` items 5–14 `n/a`, writes no planning row, and reports `partial`.

**Why.** Caught by the D10 validation run, not by review. In the first draft the pack was required at step 2, so pointing the Skill at an existing cluster with no pack ended the run before the re-verification pass could execute — and the Skill would have failed its own validation case on sequencing alone, while every rule it needed in order to pass was already written correctly.

The underlying error was treating the pack as a precondition of the whole Skill rather than of the decisions that consume it. Auditing what an existing cluster can and cannot evidence needs no new research, and is often the most useful thing the Skill can say about one.

**Consequence.** "What can this cluster still prove about itself?" is answerable as a standalone run. That is the shape the D10 validation case actually calls for.

---

## D30 — The planning record gets a write rule per stage, and state fields are not written at all — 2026-08-02

**Decision.** Two write points, both inside this Skill's own stages: **cluster decided** (end of step 8) and **brief produced** (end of step 11). Stages this bundle does not own are named in `planning-record-protocol.md` §5 without being defined. Owned fields are classified before writing: **intent** fields are written, **state** fields are not.

**Why the two write points.** The documented failure is a planning database read constantly and written to almost never, with no write rule for any lifecycle stage except the last. A single write point at the end reproduces it. Two points also mean that a run stopping between them leaves the record in a state that says so, rather than in one that looks finished.

**Why state fields are not written even when `owned_fields` names one.** This is the D2 lesson applied to a single column. A field tracking progress, position or status after handoff would be set once by this bundle, at the only moment it is present, and would then rot with no owner — the original failure in miniature. Where `owned_fields` names such a field, the Skill records a finding and leaves the field alone.

**Evidence from the validation case.** The planning record carries `Publish Status`, `Brief Status` and `Rank Math Score` alongside intent fields. One `Brief Status` cell holds a 400-character narrative including an unresolved post-publication issue — a state column being used as a log because no field owns that stage. The prediction and the artifact match.

**Boundary.** Naming the unowned stages is the whole of what is done about them. No cadence, workflow, or schedule is defined for any stage outside this bundle.

---

## D31 — Reject package 17 in full — 2026-08-02

**Decision.** Nothing from `17-metadata-and-social-markup` enters this bundle. Every candidate file was read first.

**Why.** Three independent reasons, any one sufficient.

*It is language.* Title formulas, meta-description templates, power-word lists, AIDA and PAS frameworks, and CTA patterns are wording, and wording belongs to the Skill in `authority.authority_override_skill` (policy kernel §1). This is the largest single block of language material in the source set.

*Its numbers are invented.* Brackets in a title `+38%` CTR, numbers `+20–30%`, current year `+10–15%`, question format `+14%`, and a positional CTR table quoted to one decimal place — all with no source. Policy kernel §2 forbids inventing a metric, and quoting someone else's invented metric is the same act with an extra step.

*Its method is post-publication measurement.* The A/B testing procedure — baseline CTR for 30 days, change one element, monitor 30 or more days, compare at the same average position — is performance monitoring, excluded by `architecture.md` §6.

**What was considered and still rejected.** The character budgets (roughly 50–60 for a title, 150–160 for a description) are display constraints rather than wording, and a case can be made that a brief should carry them. Rejected anyway: the brief already names the title tag and meta description as fields the voice Skill owns, and handing over a character budget alongside is how a "just the constraint" hand-off becomes a drafting hand-off. The voice Skill knows the limits of the surface it writes for.

---

## D32 — Source package cherry-pick ledger, packages 17, 18, 26, 27 — 2026-08-02

Every candidate file read before the accept/reject call. Apache-2.0 source; **no text reproduced from any of them**, per D1. Packages 26 and 27 ship the same `SKILL.md` and the same `link-architecture-patterns.md`; both were verified byte-identical and read once.

| Package / file | Verdict | Basis |
|---|---|---|
| 26/27 `site-structure-optimizer/SKILL.md` | **Reject** as a whole | Two modes at whole-site altitude — hierarchy, navigation, URL taxonomy, orphan sweeps. A different unit with a different completion criterion (`architecture.md` §2) |
| 26/27 — architecture score and structure score | **Reject** | See D25 |
| 26/27 `references/link-architecture-patterns.md` — hub-spoke required links | **Accept**, rewritten | Pillar → every spoke and every spoke → pillar is the one structural rule in the file that is checkable and is not a quota. It is `Done when` item 12 |
| 26/27 `link-architecture-patterns.md` — the five models, selection thresholds, measurement targets | **Reject** | Site-wide topology selection, and every figure in it marked `Estimated` by the source itself. A cluster does not choose a sitewide model |
| 26/27 `link-architecture-patterns.md` — migration safeguards, monthly monitoring | **Reject** | 301s and re-crawl cadence are live changes and post-publication monitoring — policy kernel §1 and `architecture.md` §6 |
| 26 `references/site-type-patterns.md` | **Reject** | URL taxonomy and depth by site type. Whole-site, and every figure `Estimated` |
| 26 `references/mermaid-templates.md` | **Reject** | Diagram templates with a colour key. Presentation, owned by the consuming project's design process |
| 27 `references/linking-templates.md` — Step 4 topic-cluster table | **Accept**, rewritten | Missing hub→spoke and missing spoke→hub as explicit columns is the right check. Re-authored around target concepts, with the anchor column removed per D24 |
| 27 `linking-templates.md` — Steps 3, 5, 6, 7 | **Reject** | Anchor wording and anchor-share thresholds (D24); navigation review (whole-site); the phased implementation plan and its tracking cadence (`architecture.md` §6) |
| 27 `references/linking-example.md` | **Reject** | Worked example of the rejected output, with a scored before/after |
| 27 `scripts/connectors/crawl.py`, `linkgraph.py` | **Reject** — not read past their purpose | Site crawler and internal-PageRank calculator. Whole-site technical tooling |
| 18 `serp-markup-builder/SKILL.md` — `schema` mode step order | Partial accept | Identify type → generate → validate is sound, and the visible-content-match rule is right. The generation and validation halves are implementation, owned elsewhere |
| 18 `references/schema-decision-tree.md` — content-to-schema mapping | **Accept** as a starting shape, corrected | The mapping question is the right question. Its rich-result column is wrong on `Service` and out of date on `FAQPage` — see D26 |
| 18 `schema-decision-tree.md` — industry recommendations, P0–P4 priority tiers | **Reject** | The tiers are a priority ranking, which is a sequencing decision this bundle does not make (D11), and the industry table is an ungrounded default |
| 18 `references/schema-templates.md`, `validation-guide.md` | **Reject** | JSON-LD blocks, validator workflows, error tables, and a monthly/quarterly maintenance cadence. Implementation and monitoring |
| 18 `schema-instructions-detail.md` — deprecation caveats | **Accept** as a pattern, re-derived | The instinct to carry deprecation warnings is right. The specific claims were re-verified independently rather than inherited, and what is encoded here is "read the documentation and stamp the read" rather than a frozen list |
| 17 — every file | **Reject** | See D31 |

**Note on the source's own strengths.** Two things in this set are better than a first reading suggests. Package 18's insistence that markup correspond to visible content is a real constraint, correctly stated, and it is carried here. And package 27's separation of contextual in-body links from navigational links is a distinction worth keeping, even though everything the source built on it was rejected.

---

## D33 — Proposal recorded, not implemented: a config key for architecture output — 2026-08-02

**Proposal.** An optional `architecture_output.path` in `project-config.schema.yaml`, matching the `research_output.path` added by D22, so the operator is not asked for an output directory at run time.

**Not implemented.** The schema is shared layer, and this task's authority covered only the four edits already made. `research_output.path` was deliberately **not** reused: it names where research output goes, and a cluster architecture record is not research output. Widening an existing key's meaning silently is worse than leaving the question open.

**Current behaviour, which is not broken.** The record is emitted in session, or written to a directory the operator supplies at run time. No path is invented. The planning-record write is unaffected — it goes to `planning_record.path`, which is already a required key.
