# Intent Classification

Owned by [`../SKILL.md`](../SKILL.md) steps 5 and 7. Every candidate is classified **twice** and both classifications survive into the pack.

**The two passes are two steps, and they are separated by the SERP reads.** Pass A (§2) is step 5 and runs from the query alone. Pass B (§3) is step 7 and runs from the SERP blocks step 6 produced. They were one step until v1.0.1, which asked for Pass B before any SERP had been observed (`docs/decisions.md` D52).

---

## 1. Why twice

A pattern read and a tool label both classify the query. The live SERP shows what the search engine has actually decided the query means. These disagree often enough that recording only one of them destroys evidence.

The classic case is a head term contaminated by a brand entity. Take a `<topic> specialist` phrase: it reads as informational from its signal words, and a national tool returns an informational class for it. Set the locality to a specific city and the same tool reports navigational, because a strong brand entity owns the term in that market. Nothing about the phrase changed. What changed is which surface was read.

So: classify from the query, classify from the SERP, keep both, and record the disagreement as a finding rather than resolving it silently.

---

## 2. Pass A — classify from the query

Four primary classes. Signal words are evidence, not proof.

| Class | The searcher wants | Signal words |
|---|---|---|
| Informational | To understand something | what, how, why, guide, symptoms, causes, explained, test |
| Navigational | To reach a specific named destination | a brand or practice name, login, hours, directions, official |
| Commercial | To compare before committing | best, top, vs, review, alternative, cost, price, which |
| Transactional | To act now | book, appointment, near me, in `<locality>`, hire, buy, consultation |

Label: `Estimated`. A pattern read is model inference and is never `Measured`.

### Sub-intent

The four classes are too coarse to specify a page format on their own. Attach one sub-intent from the list below. This is an **addition** to the four-class scheme, not established prior practice, and it is marked as such wherever it appears in output.

| Sub-intent | The query is asking | Format the SERP usually rewards |
|---|---|---|
| Definitional | What is this | Short direct answer, then depth |
| Instructional | How do I do this | Ordered steps |
| Diagnostic | Is this happening to me | Symptom and cause structure |
| Comparative | Which of these | Side-by-side, table |
| Reassurance | Is this safe, is this legitimate, what will happen | Credentials, process, what to expect |
| Provider-seeking | Who near me does this | Practitioner or location page with proof of service area |
| Access | Cost, coverage, referral, booking | Practical detail, plainly stated |

Label: `Estimated`.

---

## 3. Pass B — classify from the SERP

Only from a SERP that was actually observed. If no SERP was observed for the candidate, Pass B is `Unknown`. It is never inferred.

Read, in this order:

1. **What features are present.** A local pack is the strongest single signal that the engine treats the query as provider-seeking. An AI Overview points to definitional or instructional. A video carousel points to instructional or demonstrative. Shopping points to transactional-commercial.
2. **What kind of results occupy the top ten.** Use the result-type taxonomy in [`serp-read-protocol.md`](serp-read-protocol.md) §3. Ten directories and aggregators mean something different from ten comparable local providers, even at the same difficulty score.
3. **What format the ranking pages take.** Service page, article, directory listing, profile, forum thread, video.
4. **Whether one entity dominates.** If a single brand holds position one plus sitelinks plus a second listing, the query is at least partly navigational to that brand regardless of its signal words.

Then name the class and the sub-intent, and cite the evidence in the same line. Label: `Measured`.

---

## 4. The disagreement rule

When Pass A and Pass B disagree, **Pass B wins and both are recorded.**

The rationale is the corollary in `references/skill-contract.md` §4: validating an output against an authority that can itself be wrong is not validation. A tool's intent label is a model's opinion about the query. The SERP is the engine's decision about the query. Where a check compares two records, the one closer to the underlying reality wins, and both stay visible.

Write the disagreement as its own row, never as a resolved single value:

```
Intent (query read): Informational · Definitional — Estimated
Intent (SERP read):  Navigational — Measured, Google, <locality>, <YYYY-MM-DD>
                     — position 1 brand entity with sitelinks, brand also at position 5
Disagreement:        Yes. SERP read is authoritative. Head term is brand-contaminated.
```

A row that shows one intent value and no source has thrown away the finding.

---

## 5. What this step does not do

It does not choose a target, rank the candidates, or say which intent the client should pursue. Intent evidence is an input to that decision, and the decision belongs to `content-strategy-architect`.

It does not write the page's language. Whether a query classified as reassurance-intent should be answered with a claim about outcomes, and in what words, is decided by the Skill named in `authority.authority_override_skill`. This file names formats, not sentences.
