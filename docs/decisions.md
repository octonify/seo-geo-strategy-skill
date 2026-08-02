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

## D11 — Research produces evidence and names no target — 2026-08-02

**Decision.** `seo-geo-research` outputs a labelled evidence pack. It selects nothing, ranks nothing, and sequences nothing. `Done when` item 11 enforces this mechanically: the pack may contain no column headed `Priority`, `Score`, `Tier`, `Rank`, or `Quick win`, and no section headed `Recommendation`, `Primary keyword`, `Cluster`, `Content calendar`, or `Next steps`.

**What we take.** The reference system's separation of a survey phase from a decision phase (D1, already settled).

**What we reject, having read it.** The reference `keyword-research` Skill's delivery sections — Executive Summary, Quick Wins / Growth / GEO opportunities, Topic Clusters, Content Calendar, Next Steps — and its `Opportunity = (Volume × Intent Value) / Difficulty` formula with intent values 1/1/2/3.

**Why reject.** Both name a target from inside the research Skill. The reference system's research Skill recommends what to write, which collapses `architecture.md` §2's boundary: research is done when every candidate carries labelled metrics; architecture is done when every page has an owner and a boundary. A Skill that does both has neither completion criterion.

**Reverses if.** A consuming project runs research without ever running architecture, making the evidence pack a dead end in practice.

---

## D12 — Reject every composite priority score — 2026-08-02

**Decision.** No weighted composite score appears anywhere in this Skill. Difficulty is read as a set of separately-labelled inputs (`serp-read-protocol.md` §6), never as one number of our own construction.

**What we reject, having read it.** Four scoring models from packages 06, 07 and 11: the Priority Score matrix (volume 20% / difficulty 25% / relevance 30% / intent 15% / trend 10%, bucketed P0–P3); the Opportunity Score; the Impact × Confidence lens with BOFU/MOFU/TOFU tagging; and the Gap Priority Score with its Quick Win arithmetic.

**Why reject.** Two independent reasons, either sufficient.

First, a composite cannot carry an honest evidence label. Its inputs are a mix of `Measured`, `Estimated` and `Unknown`. Policy kernel §2 forbids presenting an estimate as measured, and a single number derived from that mix has no label that is true of it. Worse, `Unknown` inputs must be given *some* value for the arithmetic to complete — which is exactly the "`Unknown` silently becomes zero or a default" failure the kernel names.

Second, a score exists to rank candidates against each other, and ranking candidates is the decision D11 places in `content-strategy-architect`.

**What we keep instead.** Every input stated separately with its own label, plus one sentence describing what the inputs jointly show about the SERP. A reader can build any weighting they want; they cannot be handed one silently.

**Reverses if.** Architecture proves unable to decide without a pre-computed rank, across more than one real case.

---

## D13 — SERP composition is `Measured` or `Unknown`, never `Estimated` — 2026-08-02

**Decision.** A SERP was observed or it was not. A model's expectation of what a SERP probably contains is not evidence about what it contains, and this Skill has no label for it.

This is **stricter than policy kernel §2**, which permits `Estimated` for model inference generally. It narrows the permitted set for one class of metric; it adds no label and contradicts nothing.

**Why.** The observed-difficulty read is built on top of composition. An inferred composition would silently become an inferred difficulty, and a downstream Skill reading the pack would have no way to tell the difference. The same argument does not apply to a volume, where the tool name and date make the provenance visible in the value itself.

**This is an addition, not codified past practice.** The archived Gut Health research recorded SERP screenshots as evidence but had no rule preventing an unobserved SERP from being described. Flagged per the D9 pattern so it is not mistaken for precedent.

**External validation.** Search, 2026-08-02: current guidance treats tool difficulty scores as estimates that vary substantially between tools and holds that manual SERP inspection is required to catch what a score misses — a high-difficulty query whose top ten is thin, outdated, or directory-filled. That is an argument for observation over inference, which is what this rule makes non-optional.

---

## D14 — A tool-reported zero is `Unknown`, never a demand figure — 2026-08-02

**Decision.** When a keyword tool reports local volume as `0`, the pack records `Unknown — tool reports 0 for <locality>` and carries the national figure on the same row. Both lines always appear together. `Done when` item 5 enforces it: no volume cell may contain `0`.

A population-ratio figure (`national × locality population ÷ dataset population`) is permitted only as `Calculated`, only with both population inputs themselves labelled, and never in place of the `Unknown` line.

**Why.** A tool reporting zero for a locality is reporting that it has no data for that locality, not that nobody searches the term. Policy kernel §2 already forbids `Unknown` silently becoming zero; this decision names the specific mechanism by which it was happening.

**Evidence from the validation case.** The archived Gut Health keyword list holds 204 rows, of which 58 carry a blank volume and 8 carry `0`. Among them, `naturopathic doctor for gut health` is recorded as volume `0`, difficulty `0`, intent blank — and was rejected for "insufficient demand". Its locality-set SERP is populated, carries a local pack, and returns three comparable local providers in its top three. Zero data and zero demand were treated as the same fact.

**External validation.** Search, 2026-08-02: geo-modified queries in smaller markets routinely return zero from tools that carry real national volume for the same phrase, because the tool lacks per-city coverage rather than because demand is absent. The population-ratio derivation is the commonly-cited workaround, and is treated in that guidance as an estimate — which is why it is admitted here only as a labelled `Calculated` value beside the `Unknown`, not instead of it.

---

## D15 — Intent is classified twice, and the SERP wins — 2026-08-02

**Decision.** Every candidate carries two intent classifications: Pass A from the query pattern (`Estimated`, always) and Pass B from the observed SERP (`Measured` or `Unknown`, never `Estimated`). Where they disagree, Pass B is authoritative and **both are kept**, with the disagreement recorded as a finding.

**Why the disagreement is kept rather than resolved.** Directly from `skill-contract.md` §4's corollary: validating an output against an authority that can itself be wrong is not validation, and where a check compares two records, the file must state which wins. A tool's intent label is a model's opinion about a query; the SERP is the engine's decision about it. Recording only the winner destroys the finding.

**Evidence from the validation case.** `gut health doctor` returns intent `Informational` at the US dataset and `Navigational` at Kirkland, WA — the same string, the same tool, the same day. The cause is visible only in the SERP: one brand entity whose name is the query holds positions 1 (with sitelinks), 2 (its Instagram profile) and 3. A single-value intent column would have recorded one of those two labels and lost the reason for both.

**Sub-intent is an addition, flagged.** The four-class scheme is too coarse to imply a page format. A seven-value sub-intent layer (definitional, instructional, diagnostic, comparative, reassurance, provider-seeking, access) is attached and marked as an addition wherever it appears. **External validation.** Search, 2026-08-02: current guidance holds that the traditional four-intent classification is no longer granular enough and that narrower sub-intents each call for a different content format, with SERP-feature presence the most reliable secondary signal for refining the classification.

**Boundary.** Sub-intent names a format. It never names the wording. What a reassurance-intent query should be answered *with* is decided by the Skill in `authority.authority_override_skill`.

---

## D16 — Search Console query mining is a discovery source, not rank tracking — 2026-08-02

**Decision.** `seo-geo-research` may read a Search Console query export once, for the current run, as discovery source 2. It records position as an observed value at the export date. It does not establish a cadence, compare against a prior run, or report movement.

**Why this needed deciding.** `architecture.md` §6 excludes rank tracking and performance monitoring from the bundle, and a query export contains positions. The distinction drawn here is between *demand discovery* — which terms this site already receives impressions for, read once — and *position monitoring over time*, which is a separate lifecycle with a separate cadence and is the thing §6 excludes. First-party impression data is the only `Measured` demand source available to a project with no paid tool, and excluding it would have made the zero-tool path materially weaker for no gain.

**Boundary made explicit.** `keyword-universe-sources.md` §1 states the rule in the reference itself, and states that a request for movement is a different request on which this Skill stops rather than widening.

**Flagged for the coordinating agent.** This is a boundary interpretation, not a scope expansion, but it is close enough to the §6 line to be worth confirming rather than assuming.

---

## D17 — Research reads and writes no planning record — 2026-08-02

**Decision.** `seo-geo-research` does not read `planning_record.path`, `planning_record.owned_fields`, or `planning_record.row_identifier_field`, and writes no planning row.

**Why.** Policy kernel §6 governs writes into a consuming project's records and requires, among other things, that a target row be identifiable unambiguously. A research pack has no row to identify — the planning row belongs to a *page*, and a page does not exist until architecture decides one should. Giving research write access to the planning database would recreate exactly the failure D2 was drawn to avoid: two lifecycles sharing one record with no write rule.

**Consequence.** The evidence pack is the entire handoff. Architecture reads it and writes the planning row.

---

## D18 — No config key for the research output path; the operator supplies it — 2026-08-02

**Decision.** The pack is always emitted in session. A file is written only to a directory the operator supplies at run time, as `<dir>/<client.id>-<topic-slug>-keyword-evidence-<YYYY-MM-DD>.md`. No directory is assumed and no path is invented.

**Why.** `project-config.schema.yaml` defines no key for a research output directory, and that file is shared-layer foundation this task was not authorised to edit. Inventing a path would violate `skill-contract.md` §6; adding a required key would edit the foundation; making it a *required* runtime input would block a Skill that has a perfectly good in-session output.

**Recorded as a proposal, not implemented.** An optional `research_output.path` key would remove the run-time question. It is not added here. See the run report `docs/run-reports/2026-08-03-seo-geo-research.md` (filename retains the mis-stamped date per D34).

---

## D19 — Skill files carry `version: 0.0.0-unreleased` until the first tag — 2026-08-02

**Decision.** Every `SKILL.md` in this bundle carries `version: 0.0.0-unreleased` in frontmatter until a release is cut.

**Why.** `skill-contract.md` §2 requires a bundle version in frontmatter and §8 requires that all Skills share one. No tag exists: `VERSIONS.md` states that none will be cut until all three Skills pass their D10 validation case. Writing `1.0.0` into a file that is not in a 1.0.0 release would make the field a claim rather than a fact, and installed copies are supposed to be byte-identical to a tag.

**Consequence.** Cutting the first release is a mechanical find-and-replace across three files, plus the `VERSIONS.md` entry with its stated reason.

---

## D20 — Source package cherry-pick ledger, packages 06–11 — 2026-08-02

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

## D21 — Confirm D16, with the boundary tightened — 2026-08-02

**Decision.** A Search Console query export is admitted as a discovery source. The line against the `architecture.md` §6 exclusion is drawn at the **operation**, not the data source.

Permitted: a one-time read of which queries already produce impressions, used as `Measured` demand evidence at a point in time.

Forbidden, and this is what §6 excludes: retaining exports for period-over-period comparison, analysing position change, any "was 12, now 8" framing, or any scheduled re-read. A Skill that finds itself comparing two exports has left this bundle's scope.

**Why.** The exclusion in §6 targets ongoing position monitoring — a different lifecycle, a different cadence, and a different consumer. One-time demand discovery is neither. Practically, first-party impression data is the only `Measured` demand signal available to a project with no paid tool; removing it would leave the zero-tool path with no measured demand at all, and §6 was never intended to have that effect.

**Reverses if.** A consuming project acquires a rank-tracking capability whose owner should hold this data instead.

---

## D22 — Add `research_output.path` to the schema as optional — 2026-08-02

**Decision.** Approve the D18 proposal. `project-config.schema.yaml` gains an optional `research_output.path`. Coordinating-agent authority; D18 correctly declined to self-authorise a shared-layer edit.

**Why.** Not a scope expansion. The Skills already write a file when given a destination; this only removes a run-time question. Optional, so the in-session default and the never-invent-a-path rule are unchanged.

---

## D23 — `Calculated` added to the handoff evidence-basis line — 2026-08-02

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

---

## D34 — Correct the D11–D23 dates; leave run reports untouched — 2026-08-02

**Decision.** `docs/decisions.md` entries D11–D23 were stamped 2026-08-03. Every commit timestamp for that work, and the environment date throughout, reads 2026-08-02. The headings and the in-body validation dates are corrected to 2026-08-02. The run report `docs/run-reports/2026-08-03-seo-geo-research.md` keeps its filename and its contents unchanged.

**Why the two are treated differently.** `decisions.md` is a **current record**: a later session reads it to learn what is settled, and non-monotonic dates — D24 appearing to precede D23 — actively mislead. A run report is **historical evidence**: it records what was true when written, and `docs/run-reports/README.md` forbids editing one. Correcting a current record and preserving a historical one is the same principle applied to two different kinds of document.

**Origin.** The first authoring run mis-stamped itself, and the coordinating agent propagated the error into D21–D23 by following it. Recorded so the next session does not re-derive the discrepancy from the filename mismatch.

**Standing rule from here.** Date every entry from the environment date, not from a neighbouring document.

---

## D35 — Add `architecture_output.path` to the schema as optional — 2026-08-02

**Decision.** Approve the D33 proposal. `project-config.schema.yaml` gains an optional `architecture_output.path`, separate from `research_output.path`. Coordinating-agent authority; D33 correctly declined to self-authorise a shared-layer edit.

**Why.** Same shape as D22 and not a scope expansion — the Skill already writes a record when given a destination. Keeping the two keys separate is deliberate: a cluster architecture record is not research output, and quietly widening an existing key's meaning is worse than adding one.

---

## D36 â€” Source package cherry-pick ledger, package 28 â€” 2026-08-02

Every candidate file read before the accept/reject call. Apache-2.0 source; **no text reproduced from any of them**, per D1.

| Package / file | Verdict | Basis |
|---|---|---|
| 28 `protocol/entity-registry/SKILL.md` | **Reject** in full | Settled in D4 and re-confirmed rather than re-opened. Nothing was imported, adapted, or rebuilt in a lighter form. See the note below |
| 28 `entity-registry/references/entity-signal-checklist.md` | **Reject** â€” not read past its purpose | Belongs to the rejected component |
| 28 `entity-registry/references/example-audit-report.md` | **Reject** â€” not read past its purpose | Worked example of the rejected component's output |
| 28 `page-play-builder/references/local.md` â€” the canonical NAP record | **Accept**, rewritten and extended | The concept is exactly right and is the spine of this Skill. Extended with the format-decision list, the three-class difference taxonomy, and the rule that the comparison runs without a canonical (D42) |
| 28 `local.md` â€” the play sequence | **Accept** as an order, re-derived | Confirm inputs â†’ set canonical â†’ audit listings â†’ optimise profile â†’ build citations â†’ plan pages â†’ review is a sound order and is the basis of steps 1â€“8. Re-sequenced so observation precedes the canonical decision (D42) |
| 28 `local.md` â€” the GBP checklist | **Accept**, rewritten and extended | Five items in the source; thirteen here, each with an explicit four-value status vocabulary and a stated condition per value. The source's items are states worth checking; what it does not carry is a way to check them the same way twice |
| 28 `local.md` â€” "description with primary keyword in the first ~100 of 750 characters" | **Reject** | Wording, and an unsourced threshold. See D39 and D40 |
| 28 `local.md` â€” citation priority tiers | **Accept**, rewritten and extended | The tier ordering is sound. Extended with data aggregators, which the source omits entirely, and with the requirement that a source stays in the table even when it does not serve the market |
| 28 `local.md` â€” "prefer targeted precision over mass submission" | **Accept** as a direction, without a number | The direction survives external validation. Every figure attached to it in current guidance does not â€” D40 |
| 28 `local.md` â€” location and service-area page patterns | **Accept**, rewritten | Storefront versus service-area, and the no-boilerplate rule, are both correct and both externally confirmed. Re-authored around one locality per page and around what the plan may and may not decide (D41) |
| 28 `local.md` â€” "run the programmatic mode's Locations playbook alongside" | **Reject** | Generating location pages from a dataset is scaled page production. Out of scope, and the thing the duplication constraint exists to prevent |
| 28 `local.md` â€” handoff to an on-page checker | **Reject** | On-page auditing is excluded by `architecture.md` Â§6. The handoff here is to `content-strategy-architect` |
| 28 `local.md` â€” the untrusted-input rule | **Accept**, already present | Independently arrived at in this bundle's shared layer. Carried in `citation-sources.md` Â§4 for the directory-reading case specifically |
| 28 `serp-analysis/references/serp-feature-taxonomy.md` | **Reject** for this Skill | Already accepted for `seo-geo-research` in D20. A second copy in a second Skill is drift |

**On the entity-registry rejection, having read D4 again and worked the unit.** The rejection holds, and the run found a positive reason for it rather than merely no reason against it. A single location's NAP is not contested identity; it is one set of three strings written down in several places, some of them stale. What the work needs is a dated observation per place and a comparison â€” which is a flat snapshot, not an event stream. `observation-label-map.md` Â§5 states this in the Skill itself so the next session does not re-derive it. D4's "reverses if" condition â€” a client with genuinely contested identity across many locations or brands â€” did **not** fire and is not close to firing.

---

## D37 â€” The website is a NAP source, and every place it states NAP is its own row â€” 2026-08-02

**Decision.** The live site at `site.canonical_host` is observed as a NAP source alongside the profile and the directories, and it is observed **first**. Where the site states the name, address or phone in more than one place, each place is a separate row of the Observed Sources table. Structured markup carrying a NAP is its own row beside the visible text on the same page.

**Why.** The source material audits the profile and each directory and does not read the website at all. That omission hides the most consequential class of variance there is: the business's own two first-party surfaces disagreeing with each other. A directory being stale is somebody else's copy going out of date; the site and the profile disagreeing is the business making two different statements about itself, and only one of them can be right.

One row per site is not enough either. A footer, a contact page, a schema store and a map widget are separate stores edited at separate times, and a single site-level row records whichever one was looked at while presenting it as the site's position.

**Evidence from the validation case.** The consuming project emits its NAP from seven distinct stores. Its own cross-check found four of them carrying a designator the other three did not, in three different casings. A one-row-per-site model would have recorded one of those and called the site consistent.

**This is an addition, not codified past practice.** Flagged per the D9 pattern so it is not mistaken for precedent.

**Consequence.** `Done when` item 2 requires the site to be a row and requires each NAP-bearing place to be its own row. It is the item that makes a site-versus-profile mismatch surface mechanically rather than by whoever happens to notice.

---

## D38 â€” An unchecked source is `Unknown`; no local-presence observation is ever `Estimated` â€” 2026-08-02

**Decision.** Two rules, one reason.

`present-correct`, `present-wrong` and `missing` are observations. `missing` means a check was run and no listing was found. A source nobody checked is `Unknown â€” not checked`, with the reason, and `Done when` item 9 forbids an unchecked source being recorded as `missing`.

And no observation in this Skill carries `Estimated`. Every value in the record is a string somebody published or a comparison between two such strings. On a well-formed run the `Estimated` count is `0`, and a non-zero count is a defect rather than a variation.

**Why.** These are policy kernel Â§2's "`Unknown` never silently becomes a default" applied to the two mechanisms by which it was going to happen here. A citation table is a natural to-do list, and a to-do list marks unchecked things as absent, because absent is what you do something about. That turns a thin audit into a confident-looking one: work is sent at listings that already exist, while the directories nobody opened stay invisible behind a table that appears complete.

The `Estimated` half is **stricter than policy kernel Â§2**, which permits `Estimated` for model inference generally. It narrows the permitted set for one class of observation; it adds no label and contradicts nothing. This is the same move D13 made for SERP composition, for the same reason: there is nothing here for a model to infer, and a label permitting inference would let an unopened directory be described.

**External validation.** Search, 2026-08-02: current guidance holds that inconsistent listings split entity resolution and that duplicate listings are common and damaging â€” an argument for checking each source, and against a table that reports on sources it never opened. The specific figures quoted alongside that guidance were not encoded; see D40.

---

## D39 â€” Presence is checked; wording is not, including the profile description â€” 2026-08-02

**Decision.** The GBP checklist records that a description exists and how long it is. It does not evaluate it, score it, check it for a term, or draft a replacement. The same holds for every language field the record names: they are named, with their owner, and never filled.

**What we reject, having read it.** The source material's instruction to place the primary keyword within the first hundred characters of the seven-hundred-and-fifty-character description.

**Why reject.** Two independent reasons, either sufficient. It is a wording instruction, and policy kernel Â§1 gives wording to the Skill in `authority.authority_override_skill` â€” the same line D24 drew for anchor text and D31 drew for titles and meta descriptions. And the threshold is an unsourced figure of the kind D31 rejected.

**External validation.** Search, 2026-08-02: current guidance holds that the profile description is **not** a direct ranking input, contributing to profile completeness and to answer-engine summaries rather than to position. So the rejected instruction is not merely out of scope here; the premise underneath it is weaker than it sounds.

**The boundary is not "no opinion about the profile".** Guideline compliance is checked and is a finding: a name field carrying a tagline, a store code, or opening-hours text is `present-wrong` with the observed string quoted, because the platform's own documentation says what a name field may contain. What the name should say instead, where a choice exists, is language and goes to the voice Skill. This Skill names the constraint; that Skill writes inside it.

---

## D40 â€” Every unsourced local threshold is rejected, and the direction underneath it is kept â€” 2026-08-02

**Decision.** No number enters this Skill that its source cannot ground. The class is rejected once here rather than argued four times.

**What we reject, having read it.** Read on 2026-08-02, across the source material and current external guidance:

| Rejected figure | Where it appeared |
|---|---|
| A target citation count â€” a band of forty to eighty, "thirty accurate beat two hundred poor", "ten beat fifty" | Citation guidance |
| A share of consumers who lose trust over inconsistent details | NAP consistency guidance |
| A citation-count comparison presented as a routine outcome | NAP consistency guidance |
| The share of shared content at which duplicate-detection fires, and the share of a page that must be unique | Location-page guidance |
| A number of pages to publish per week, and a count of cities worth targeting | Location-page guidance |
| Keyword position within the first hundred characters of a description | The source material â€” also rejected on D39's first ground |

**Why.** Policy kernel Â§2 forbids inventing a metric, and quoting somebody else's invented metric is the same act with an extra step â€” D31 settled this and it transfers unchanged. These are worse than most in one respect: they are stated to the point, which makes an unsourced convention read as a measurement, and they concern a system nobody involved can observe.

**What we keep instead.** The direction, where external validation supports it and only as a direction. Accuracy across fewer sources is reported to outperform volume across many. Near-duplicate location-page sets are treated as scaled content abuse and can be deindexed as a set. Both are encoded as constraints on what the record must contain, with no threshold attached.

**The one distribution the bundle does carry is carried as context, not as arithmetic.** External guidance read 2026-08-02 attributes roughly a third of local pack weight to profile signals in aggregate â€” around 32%, up to 36% in one source. That is D3's premise and it is confirmed. It is recorded in `gbp-checklist.md` Â§5 as third-party reporting about an unobservable system, explicitly not as a calculation anyone should perform against an individual profile.

---

## D41 â€” Local presence plans pages, decides no target, and writes no planning row â€” 2026-08-02

**Decision.** The Page Plan names which location and service-area pages should exist, which single locality each owns, its disposition, and the structural elements it must carry. It decides nothing about what any page ranks for, and it writes no row into `planning_record.path`.

**Why the target decision stays out.** `architecture.md` Â§2 gives page ownership to `content-strategy-architect`, whose completion criterion is that every page has an owner, a boundary and a link target, reached from an evidence pack. A location page is a page. Deciding its term here would put the same decision in two Skills with two completion criteria and no rule for which wins â€” and it would be made without the pack, on a locality name.

**Why no planning row.** D17's reasoning transfers unchanged. Policy kernel Â§6 requires a target row to be identifiable unambiguously, and a planning row belongs to a page that architecture has decided should exist. A page this Skill proposes has not been through that decision yet. Two Skills writing the same row from different lifecycles is the failure D2 was drawn to avoid.

**Consequence.** The Page Plan is an input to `content-strategy-architect`, which may hold or re-scope a page on evidence this Skill does not carry. `location-page-plan.md` Â§3 states it: the plan proposes pages, it does not reserve them.

**A gap found and not filled.** Neither `seo-geo-research` nor `content-strategy-architect` produces the list of localities a business serves, and `project-config.schema.yaml` has no key for one, so it arrives from the operator every run. Recorded as a proposal in D45, not implemented.

---

## D42 â€” The variance comparison runs without a canonical, against a named base â€” 2026-08-02

**Decision.** Comparing the observed sources against each other does not require a canonical NAP. Where none was agreed, the first Observed Sources row â€” the site's primary NAP surface â€” is designated the **comparison base**, every other source is compared against it, and the variance table states at its head that the base is a base and not a canonical.

`Done when` items 4, 5 and 6 therefore never read `n/a`. Only items 3, 11 and 12 may, and only on an observation-only run.

**Why.** Caught by the D10 validation run, not by review. In the first draft the whole comparison hung off the canonical, so a consuming project with no declared canonical took the observation-only path and the variance table was excused â€” leaving the run's central finding sitting as two rows of a transcription table for a reader to notice by eye. The Skill would have failed its own validation case while every rule it needed in order to pass was already written correctly.

This is D29's fault in a second Skill, and the underlying error is the same one: treating a decision as a precondition of the observations that inform it. Auditing what a presence currently says needs no agreement about what it should say, and is usually the most useful thing to be able to say about one.

**Why the site is the base, stated openly.** It is the surface the business most directly controls and can change without a third party's approval, which is a reason to compare *from* it. It is not a claim that it is correct, and a variance row does not mean the other source is wrong. An agent never derives a canonical from the observations by majority, recency, or authority â€” a count of directories is not evidence about a business's own name.

---

## D43 â€” A dated observation from an earlier session is carried with its date, never as current â€” 2026-08-02

**Decision.** Where the only available observation of a source is one made in an earlier session, it is carried with its original date and its original surface, its row reads `as at <date>, not re-observed this run`, and the source's **current** state is listed in the Unknowns table.

**Why this needed deciding.** Both alternatives are wrong in a way that is easy to miss. Presenting a four-day-old string as the profile's current value states a fact nobody checked. Discarding it because it is not fresh leaves the comparison unmade, which throws away the only evidence there is and reports `Unknown` where a real, dated finding was available.

The generalisation is the one already in `metric-label-map.md` for research metrics, moved one step: an observation is evidence about **its own date** and about no other. A local presence changes when somebody edits it, which makes staleness a first-class property of every row rather than an edge case.

**Evidence from the validation case.** The consuming project's only profile observation was four days old and had been superseded on the same day it was made â€” the profile was aligned to one designator in the morning and the site was moved to a different one that afternoon, by two separate instructions. A rule that discards stale observations would have reported the profile as `Unknown` and missed the divergence entirely; a rule that presents them as current would have asserted a profile state that no longer had to be true.

---

## D44 â€” Reviews are not checked here, and the gap is recorded rather than filled â€” 2026-08-02

**Decision.** Reviews, ratings, review velocity, and replies are outside this Skill. So are posts, offers, questions and answers, messaging, and profile performance insights. Each is listed in `gbp-checklist.md` Â§4 with its reason, so the absence is visible in the Skill rather than inferred from its silence.

**Why, per exclusion.** Replying, posting, and responding are live changes to an external surface â€” policy kernel Â§1, without exception. Performance insights are post-publication measurement â€” `architecture.md` Â§6. Reviews and ratings are a continuously-changing state with their own lifecycle, and D2's rule keeps that out of a record whose other fields are one-time decisions; a review count written once into a snapshot is the state-column rot D30 described, arriving through a different door.

**The honest part.** External guidance read 2026-08-02 places review signals second only to profile signals in local weight, at roughly 16%. So this is a real gap in coverage, not a category nobody needs, and calling it out of scope does not make the need go away. It is recorded as a proposal in the run report and is **not** implemented: adding it requires the scope-expansion rule in `architecture.md` Â§5 â€” external validation plus explicit operator approval â€” and the external validation half is now done.

**What would satisfy it, if approved.** Not a field inside this record. A separate unit with its own completion criterion and its own cadence, which is what its lifecycle actually calls for.

---

## D45 â€” Proposals recorded, not implemented: a service-area list and a local-presence output path â€” 2026-08-02

**Proposal one.** A `local_presence.service_areas` list in `project-config.schema.yaml`. `service_area_mode` already declares *whether* a business serves areas rather than a storefront; nothing declares *which* areas. The Page Plan needs that list on every run, and it arrives from the operator every run.

**Proposal two.** An optional output-directory key for this Skill's record, matching `research_output.path` (D22) and `architecture_output.path` (D35). Neither of the existing two is reused: a local presence record is neither research output nor an architecture record, and quietly widening a key's meaning is worse than leaving the question open â€” the reasoning D33 gave and D35 upheld.

**Not implemented.** The schema is shared layer, and this task's authority covered exactly one commit of edits already on disk. Proposing a third path key immediately after the second was approved is also the point at which the pattern is worth settling once rather than one Skill at a time.

**Current behaviour, which is not broken.** Service areas are supplied by the operator at run time and the record names who supplied them. The record is emitted in session, or written to a directory the operator supplies at run time. No path is invented and no locality is assumed.

---

## D46 — One `outputs` block, one key per Skill, settled once — 2026-08-02

**Decision.** `research_output.path` and `architecture_output.path` are consolidated into a single `outputs:` block carrying one key per Skill, named for the Skill's directory. `local-presence-manager` gets its key in the same change. The convention is stated in the schema: **a new Skill adds one key here and nothing else.**

**Why.** Three separate path keys were added in three separate runs (D22, D35, D45), each correctly declining to reuse its predecessor and each requiring its own decision. The reasoning was right every time and the outcome was still three top-level blocks with no stated pattern. Three instances is where a convention is cheaper than a fourth debate.

The no-sharing rule that produced the separate keys is **preserved, not reversed** — it is now written into the block itself rather than re-derived per Skill.

**Why now.** Zero consuming projects have this bundle installed. Consolidating costs only two key renames inside this repository; after the first install it would cost a migration in every consumer. This is the cheapest this change will ever be.

**Consequence.** `seo-geo-research` and `content-strategy-architect` reference the old key names and must be updated to `outputs.<skill-name>.path`. Carried as a follow-up.

---

## D47 — `local_presence_extra.service_areas` added — 2026-08-02

**Decision.** Approve the first half of D45. The schema gains an optional service-area list.

**Why.** The location page plan needs it on every run and it arrives from the operator on every run. Same shape as D22 and D35: not a scope expansion, just removing a repeated run-time question.

---

## D48 — Review checking is approved in principle, deferred to v1.1 — 2026-08-02

**Decision.** D44's proposal is **not** implemented in v1.0.0. The gap is real and the argument for it is accepted; the timing is not.

**Why the gap is real.** External validation is complete and reported roughly 16% of local pack weight, second only to profile signals. That is the same class of argument that put local presence into v1 at all (D3). It is not rejected on merit.

**Why v1.1 and not v1.0.0.** Two reasons that have nothing to do with the merit. The agreed deliverable was three Skills, and adding a fourth before any of the three has been used on a real task is building on unvalidated ground. And `architecture.md` §5 requires explicit operator approval for scope expansion; the coordinating agent may confirm a boundary interpretation (D21) or approve a schema key (D22, D35, D47), but adding a Skill changes the agreed deliverable and is not its call to make alone.

**Shape, when it is built.** A separate unit with its own completion criterion, per D44's own recommendation — not a field inside the local-presence snapshot. A review count written once into a record that nothing updates is exactly the state-column rot D30 documents.

**Reverses if.** The operator asks for it in v1.0.0, or first real use shows the local-presence record is not actionable without it.

---

## D49 — The release run's shared-layer de-identification is ratified — 2026-08-02

**Decision.** The two edits made under the release task's own authority stand, and the reading of `skill-contract.md` §6 that produced them is adopted as the standing one.

**What happened.** The pre-release conformance pass found `references/policy-kernel.md` §1 naming a real consuming client's voice Skill, and six `example:` fields in `project-config.schema.yaml` carrying one client's slug, business name, live domain, city, and service-area list. Both were fixed before tagging, and the run declared the edit rather than performing it silently.

**Ratified, and why.** Both were introduced by the coordinating agent when the shared layer was authored, and neither was caught by the two earlier per-Skill conformance passes because both files sit outside `skills/`. The run's own reasoning is correct: §6's letter governs Skill files, but a bundle built for many consumers must not carry one client's domain and business name into every other install. This is the third instance of the same class, after the worked example de-identified in `intent-classification.md`.

**Standing rule.** §6 is read as covering **every file that ships in an install set**, not only files under `skills/`. The install set is `references/`, `skills/`, `CLAUDE.md`, `AGENTS.md`, `LICENSE`, `project-config.schema.yaml`. Files under `docs/` are outside it and keep their real client references, because they are validation evidence and de-identifying them would destroy the proof that validation happened.

**Reverses if.** Nothing foreseeable. The rule only widens what is already required.

---

## D50 — `local-presence-manager`'s out-of-brief edit is ratified — 2026-08-02

**Decision.** The release run updated a third Skill under a follow-up whose brief named two. The edit stands.

**Why.** D46 and D47 changed the schema. `local-presence-manager` carried both superseded key names and a sentence asserting that no config key existed for a local-presence output directory — which D46 had just made false. Leaving it would have shipped a Skill contradicting the schema it reads. And `local_presence_extra.service_areas` had nothing reading it: a config key no Skill consults does not remove a run-time question, which is the entire stated purpose of D47.

The edits are inside the letter of D46 and D47 and outside the letter of the brief's step. The run flagged that rather than quietly widening its scope, which is the behaviour the drift rules are for.

**Standing rule.** A follow-up that enumerates files is read as naming the ones known to need the change, not as forbidding a fourth that demonstrably does. A file left asserting something a just-approved decision has made false is a defect, not scope discipline. Report the extra file; do not leave it wrong.

---

## D51 — The architect's pack-consuming path is untested and must be exercised first — 2026-08-02

**Decision.** Confirm the release run's characterisation of `content-strategy-architect`'s limitation. It is derived rather than quoted, and it is correct and material.

**What it means.** That Skill's D10 case ran as a **re-verification-only** run: no evidence pack existed for the validation cluster, gate 3 fired, and the run proceeded down the inherited-decision path. It reached a real finding there — 35 of 35 rows carrying a declared primary keyword and none carrying a snapshot, source, or rejected alternatives — and the gate behaved correctly.

But the Skill's **main path** was not exercised against real data: primary-keyword selection from a pack, the cluster map, the link map, the schema table, the briefs, and the planning-record write. Untested is not known-broken, and it is also not validated.

**Consequence, and this is the operative part.** The first real run must exercise exactly that path: run `seo-geo-research` first to produce a genuine pack, then feed it to `content-strategy-architect`. A first real run that skipped the pack would re-test the one path already covered and leave the untested one untested through a second cycle.

The expected stop at the planning-record write, caused by the consuming project having no row-identifier column, is designed behaviour and does not make such a run a failure. Everything upstream of that write is what needs exercising.

---

## D52 — Fix the four faults the first production run found — 2026-08-02

**Decision.** F2, F3, F6 and F5 from `seo-geo-strategy-first-run-2026-08-02.md` are accepted as real and are fixed in v1.0.1. F1 and F4 are accepted as wording clarifications in the same release. F7 and F10 are deferred.

**F2 — a third sequencing fault, same class as D29 and D42.** `seo-geo-research` step 5 requires Pass B "from the observed SERP" while SERPs are first observed at step 6. Followed literally, Pass B is impossible when it is asked for. The run executed the only possible order and said so.

This is now three for three: every Skill in this bundle shipped with a step that required output from a step that had not run yet, and every one was found by execution rather than by reading. **The pattern is not coincidence and the contract should carry a check for it.** `skill-contract.md` gains a requirement: each procedure step names its inputs, and no step may name an output produced by a later step. That is mechanically checkable from the Skill file alone, so it fires at authoring time rather than on first production run.

Fix: split step 5 into 5a (Pass A, from the query, before the reads) and 5b (Pass B, from the SERP, after them).

**F3 — partial observation is undefined on both sides of the handoff.** The read protocol handles a read missing its date, locality, or surface, but `Done when` items 7 and 8, and the architect's overlap rule, know only observed and not-observed. A SERP with 4 of 10 positions captured is neither, and the run had to improvise at precisely the point the policy kernel says to stop and report. It reported, correctly.

Fix: the overlap rule gains a third row — either SERP observed below a stated position count makes the pair `Unknown`, never split. The read protocol gains `partial` as a first-class observation state with the captured position count recorded.

**F6 — `Done when` item 1 contradicts gate 2.** Item 1 forces `stopped` when any required key is missing; `row_identifier_field` is required; gate 2 option 3 produces the full record with the write `stopped` and overall `partial`. Under the literal reading, option 3 is unreachable. The run took the only interpretation that makes the gate's own option exist.

Fix: scope item 1 to required keys **whose absence does not have its own gate**.

**F5 — an enforced count with no definition.** Both Skills require the evidence-basis totals to equal the count of labelled values, but nothing says what one labelled value is. The run defined a rule, scripted it, and stated it beside the counts — which is honest and also means a second operator would define a different rule and both would pass. An unenforceable check that reports as enforced is worse than no check.

Fix: `skill-contract.md` §5 defines the counting rule once, for all Skills.

**F1 and F4 — wording.** Gate 3 reads as being about the channel; an authenticated-but-unreadable tool needed inference to classify. Reword to "the named tool cannot actually be read: not connected, not authenticated, or not reachable". And step 2's inherited-decisions pass is written for existing pages; the run correctly treated planning rows that declare a primary keyword as inherited decisions and surfaced three undocumented ones. Say so explicitly.

**Deferred.** F7 (per-member selection trails) is a template improvement with a working alternative in place. F10 (no staleness threshold on the schema snapshot) needs a real second read before a threshold can be chosen honestly.

**Reverses if.** Nothing foreseeable. Every item traces to an observed execution.

---

## D53 — The line-ending difference between repo and install is expected — 2026-08-02

**Decision.** An installed file whose bytes differ from the working-copy bytes **only** by line endings is correctly installed. Byte-identity is asserted against the **tag's blob hashes**, not against a Windows working copy.

**Why this is recorded.** Verifying the install, the coordinating agent found a raw `sha256` mismatch on a shared-layer file and had to establish whether the install had drifted. All 26 files are content-identical; the repository working copy is CRLF and the install is LF, because the install deliberately used `core.autocrlf=false core.eol=lf` after a first attempt silently rewrote every file.

Without this note, every future install verification re-derives the same scare.

**The rule.** Compare an installed file to `git ls-tree` blob hashes, or compare content with line endings normalised. A raw byte comparison against a Windows working copy is not a valid check and will always appear to fail.

---

## D54 — `access_mode` for the first consumer moves to `manual_paste` — 2026-08-02

**Decision.** Accept F8. The consuming project's `research_tools.access_mode` changes from `browser_agent` to `manual_paste`. This is a **consumer config change, not a bundle change**; the bundle supports all three modes and none of them is at fault.

**Why.** Two independent observed reasons. No authenticated session for the named tool exists in the browser, so the tool serves its logged-out page and the run consumed a free-checker quota on mechanics alone. And the browser renderer froze repeatedly on ordinary result pages: roughly a third of captures needed retries, two reads stayed partial, and one completed only via a lighter view.

`browser_agent` was set on the strength of "the agent can work with the tool through a browser", which is a statement about capability. `access_mode` describes what is reliably available at run time. Those are different claims and the first run separated them.

**Reverses if.** An authenticated session is established and renderer stability is demonstrated across a full run.

---

## D55 — The anti-sequencing check, and integer renumbering rather than 5a/5b — 2026-08-02

**Decision.** `references/skill-contract.md` §3 gains the rule D52 specified: each procedure step names its inputs, and no step may name an output produced by a later step. Applying it, `seo-geo-research`'s procedure is renumbered **1–13 with plain integers**, not 1–12 with a split 5a/5b.

**Why integers.** D52 describes the fix as "5a (Pass A) and 5b (Pass B)", and the two halves land either side of the SERP reads. Keeping those labels literally would have put the procedure in the order 5a, 6, 5b, 7 — and the new rule is stated in terms of *later*, which that ordering makes ambiguous exactly where the check needs to be sharp. A rule that says "no step names a later step's output" needs a procedure whose step numbers and whose execution order are the same sequence. So Pass A is step 5, the SERP reads are step 6, Pass B is step 7, and everything below shifts by one.

The split D52 asked for is the substance and it is intact: two steps, separated by the reads, each naming its own inputs and its own labels. Only the labels differ from D52's shorthand.

**The second half of the rule cost more than the first.** "Each step names its inputs" means every step in all three Skills gained an `*Inputs:*` line — 37 steps. That is the part that makes the check mechanical: with inputs declared, verifying the ordering is reading two lines per step, and it no longer depends on inferring what a step needs from its prose.

**What the full pass found.** One fault, the one D52 already named. `content-strategy-architect` and `local-presence-manager` both pass; every step's inputs resolve to step 1's config, the operator's material, an observed surface, or a lower-numbered step's output. Recorded because "we checked and found nothing" is only worth anything if it was written down at the time.

**Reverses if.** Nothing foreseeable.

---

## D56 — The overlap test's position floor is 8 of the top ten — 2026-08-02

**Decision.** In `cannibalization-guardrails.md` §2.1, a `partial` SERP read below **8 of the top ten captured** cannot decide an overlap pair; the pair is `Unknown` and is not split. Above the floor the count is used, and the record carries both captured counts.

**Why 8, and why a floor rather than a formula.** The threshold of 4 shared URLs was set against a ten-result surface. Counting shared URLs across a four-position capture is not a stricter reading of that rule — it is the same numerator over a different denominator, and it quietly makes the convention mean something it was never set to mean. The floor is the point where the captured slice is still close enough to ten that the convention applies to it. At 8 or more per side, at most two positions per side are unseen, so the observed shared count understates the true one by at most two — a bound small enough to quote. Below 8 there is no bound worth quoting: a four-position capture leaves six unseen and says nothing about whether the pair crosses 4.

**The asymmetry is the operative part.** Unseen positions can only *raise* a shared count. So:

- a count already **≥ 4** on reads at or above the floor is safe — it cannot fall back under the threshold, and the pair goes to **one page**;
- a count **≤ 3** on any read short of a full ten is **`Unknown`**, not a split — the unseen positions could carry it over.

A partial read can therefore send a pair to one page and can never send it to two. That is the same direction §2 already fixed for an unobserved SERP, for the same reason: a wrong split is live and hard to unwind; a wrong hold costs a page that was not built yet.

**Considered and rejected.** A per-pair formula — permit the split only when `observed shared + min(unseen either side) ≤ 3` — is more precise and is what the arithmetic actually implies. It was rejected because D52 asked for a stated count, because a rule an operator has to evaluate per pair is a rule that gets approximated, and because the asymmetry above already delivers the formula's protection in the only direction that matters.

**Reverses if.** A real run shows the floor holding pairs that a full read would have split, often enough to matter — which the record can show, because every `Unknown` row names which read fell short and by how much.

---

## D57 — The evidence-basis counting rule belongs to the contract, once — 2026-08-02

**Decision.** `references/skill-contract.md` §5 defines what one labelled value is, for all three Skills. One labelled value is one occurrence of one of the five label words at a position where it labels a value; the inclusion and exclusion lists are in that section. `metric-label-map.md` §4 and `observation-label-map.md` §4 now point at it instead of restating the requirement without a definition.

**Why here and not per Skill.** F5's finding is not that the first run's counting rule was wrong — it was reasonable, it was scripted, and the run stated it beside the counts, which is more than the contract asked for. The finding is that stating it was *necessary*, and that a second operator would have stated a different one and also passed. A `Done when` item that reports `Pass` under two incompatible definitions is not enforcement; it is enforcement-shaped.

**The rule names its own edge cases on purpose.** A row with a `Label` cell and two `Unknown — <reason>` value cells counts three, not one and not two. An empty `Label` cell counts nothing and is a defect in the row. `Unknown` counts like the other four. Those three sentences are where two honest operators would otherwise diverge, and a rule that leaves its divergence points implicit has not fixed anything.

The Skills are now told not to state a counting rule beside their totals. Stating one invites it to disagree with this one.

**Reverses if.** A deliverable shape appears that the inclusion list cannot classify. Then the list gains a row here, not a local rule there.

---

## D58 — `local-presence-manager` gets F6's fix too — 2026-08-02

**Decision.** The `Done when` item 1 scoping that D52 specified for `content-strategy-architect` is applied to `local-presence-manager` as well. `seo-geo-research` is left alone.

**Why.** F6 is a contradiction between "any required key missing means `stopped`" and a gate whose own option produces something other than `stopped`. `local-presence-manager` has the same contradiction three times over: gate 2 option 3 produces an observation-only run reported `partial` when `local_presence.canonical_nap` is absent; gate 6 option 2 proceeds with every GBP row `missing — no profile found`; gate 7 option 2 proceeds on the observed state. All three keys are required, and under the unscoped item 1 all three options are unreachable.

D50's standing rule governs: a follow-up naming files names the ones known to need the change, and a file left asserting something a just-approved decision has made false is a defect rather than scope discipline. F6 was found in one Skill because that is the Skill the first run exercised, not because it is the only one that has it.

`seo-geo-research` is untouched because it has no such key: its gate 1 option 3 stops, which is what item 2 already says. Adding a clause with nothing to point at would be noise.

**Reverses if.** Nothing foreseeable.
