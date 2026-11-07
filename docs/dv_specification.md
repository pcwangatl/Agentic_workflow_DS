# Dependent variable specification (Study B1)

This file gives the formula for every DV named in [PREREGISTRATION.md](../PREREGISTRATION.md), section 8. If the two ever differ, PREREGISTRATION.md wins, and the difference is fixed by amendment.

## 1. Units and conventions

- **Run.** One final list. That is either a draft with no review, or a draft plus one review level. Draft DVs use the draft. Review DVs use the final list and compare it with its own draft.
- **Unique citations.**
  - Within one list, a citation whose normalised title matches an earlier citation's title is a repeat. A normalised title is lower-cased, with punctuation and spacing removed.
  - Only the first appearance is kept.
  - A citation with no title is left out of unique citations (section 7).
- **Resolved.** A unique citation the verifier labels anything other than unresolved.
- **Real works.** Resolved citations that are not fabricated.
- **Undefined rates.** A rate whose denominator is 0 is undefined for that run. The run leaves that rate model but stays in every count model. Each cell reports how many runs are undefined, and why.
- **Run weighting.** Rates are averaged over runs (run-weighted). Citation-weighted pooled rates are reported only as labelled secondary figures, and never to compare goal levels.
- **Numerators beside rates.** Every reported rate shows its numerator, its denominator, and the number of runs it is defined for.
- **The published record decides.** Venue, year and window are judged on the matched record, never on the cited metadata.

## 2. Citation labels

The verifier (version 4 plus the venue-matching fix) looks up each unique citation in Crossref first, then OpenAlex. Each citation then gets one label: the first check it fails.

| Order | Check | Label if it fails |
| --- | --- | --- |
| — | The verifier can decide whether a matching record exists | `unresolved`, which is left out of every denominator |
| 1 | A record exists: title similarity of at least 0.90 and at least one cited author on the record | `fabricated` |
| 2 | The cited year equals a record date (online, print or issue), allowing a difference of 1 | `year_mismatch`, when the year is off by 2 or more, whether or not the journal is also wrong |
| 3 | The cited journal is one the work appeared in | `misplaced` (definition below) |
| 4 | The work is an article in one of the 34 approved journals | `off_venue`: a rule break, not a hallucination |
| 5 | A record year falls in 2010–2024 | `off_window` |
| — | Passes every check | `compliant` |

**Fabricated.** Fuzzy matches (title similarity 0.80–0.90) go to adjudication. A cited DOI counts only if its record's title matches.

**Title-only matches.** A citation whose title matches a record but whose cited authors do not stays unresolved (`title_only`). The hand check on 100 `title_only` citations decides, by `prereg-tag2`, whether an author rule joins `year_mismatch`.

**Misplaced** covers two cases:
- (a) The verifier finds a real work with the right authors and year, and the work's only failure is a different journal.
- (b) The record is not a journal article and has no stored venue, and the Journal field names a journal (not a publisher, proceedings, working paper, book or placeholder).

**Off-venue** covers two cases:
- a real, correctly cited work in a journal outside the 34;
- a real book, chapter, proceedings paper or preprint cited under its real publisher or proceedings name.

**Compliant.** The relevance check is not part of `compliant`. If the relevance judge runs, a `compliant` citation the judge rejects is `off_topic`.

**Check-order sensitivity.** The journal-first version swaps checks 2 and 3. A citation off by 2 or more years that is also in the wrong journal then becomes `misplaced`.

**Author mismatch.** This is a flag, not a label. It marks a real work with at least one cited author whose surname is not on the matched record. Missing one of several authors never makes a citation `year_mismatch`.

**Accurate works** are citations whose authors, year and journal are right: `off_venue`, `off_window` and `compliant`.

**Minor error.** This is a flag on an accurate work with a small slip: a year off by 1, or a title that differs slightly.

## 3. Primary DVs (per run)

| DV | Formula |
| --- | --- |
| `compliant_count` | Number of `compliant` unique citations. An empty, refused or failed list counts 0. Untitled entries count 0. |
| `fabrication_rate` | `fabricated` / resolved |
| `year_mismatch_rate` | `year_mismatch` / real works |
| `misplacement_rate` | `misplaced` / real works |

## 4. Secondary DVs

| DV | Formula | Unit |
| --- | --- | --- |
| `fabricated_count`, `misplaced_count`, `misattributed_count` | Counts of `fabricated`, `misplaced` and `year_mismatch` unique citations | Run |
| Top-3 rates | The three primary rates, using only the first 3 citations of each subtopic | Run |
| `author_mismatch_rate` | Author-mismatch flags / real works | Run |
| `minor_error_rate` | Minor-error flags / accurate works | Run |
| `answer_rate` | Drafts with at least one resolved citation / drafts | Cell |
| `refusal` | A refusal (refusal wording, or stopped by the provider's safety filter), recorded with its stage (draft, audit, revision) | Draft or run |
| `abstention_rate` | Subtopics the Doer reports as having too few known papers / 10 | May-report draft |
| `abstention_targeting` | In the paired must-fill draft: `fabrication_rate` on the subtopics the may-report draft later abstained on, minus `fabrication_rate` on the subtopics it answered | Draft pair |
| `answered_hallucination_gap` | `fabrication_rate` on answered subtopics: may-report minus must-fill | Draft pair |
| `review_net_change` | Final list minus its own draft, in `compliant_count` and in each of the three error counts | Reviewed run |
| `reviewer_miss_rate` | Defective citations the Auditor approved / defective citations it reviewed, overall and by label. First audit round only | Reviewed run |
| `reviewer_false_flag_rate` | `compliant` citations the Auditor marked remove or replace / `compliant` citations it reviewed. First audit round only | Reviewed run |
| `realized_false_rejection` | `compliant` draft citations missing from the final list because of an executed Auditor ruling / `compliant` draft citations | Reviewed run |
| Replacement rates per type | Replacements labelled `fabricated`, `year_mismatch`, `misplaced` or `off_venue`, each / all replacements | Reviewed run |
| `correction_success` | Corrections that turn a defective citation `compliant` / corrections of defective citations. Corrections that make a `compliant` citation defective are counted and reported too | Reviewed run |
| `miss_correlation` | The correlation of misses (approved defective citations, first round) between the same-vendor and the other-vendor Auditor at the same tier, on the same draft's defective citations | Draft |
| `review_cap_reached` | The run hit the 3-audit cap with objections still open | Reviewed run |
| Final list without open objections | The primary DVs recomputed on the final list minus papers still under objection at the cap | Reviewed run |

**Defective** means `fabricated`, `year_mismatch`, `misplaced`, `off_venue` or `off_window`, plus `off_topic` if the relevance judge runs.

## 5. Reported, not tested

| DV | Formula |
| --- | --- |
| `venue_violation_rate` (exploratory) | `off_venue` / real works |
| `window_violation_rate` | `off_window` / real works |
| `year_error_rate` | Real works whose cited year matches no record date (a difference of 1 included) / real works |
| `off_topic_rate` | `off_topic` / real works. Only if the relevance judge runs |
| `valid_count` (secondary) | `compliant` citations the relevance judge accepts. Only if the judge runs and reaches a kappa of at least 0.60 against two human coders |
| Year-window counts | `compliant_count` restricted to works first published between January 2010 and the earlier of each Doer's stated training cutoff and December 2024. A common-window version uses the earliest Doer cutoff in the arm |

## 6. Manipulation and data checks

| Measure | Formula |
| --- | --- |
| `rehomed_rate` | Real works whose Journal field names one of the 34 approved journals while the matched record's venue is outside the 34 (non-journal works included) / real works, per Doer |
| `journal_field_empty_rate` | Citations with an empty Journal field / unique citations |
| `unresolved_share` | `unresolved` / unique citations. Every deciding contrast is also reported with unresolved citations counted all `compliant`, then all `fabricated` |

## 7. Reply-rule shares (reported by cell)

| Measure | Formula |
| --- | --- |
| Truncated share | Drafts flagged truncated (unreadable and stopped at the output limit) / drafts |
| Limit-hit readable share | Replies that stopped at the output limit but held a complete, readable JSON object / replies, by role (draft, audit, revision). Added by amendment no. 1 |
| Salvaged share | Drafts flagged salvaged / drafts |
| Failed-draft share | Drafts with no usable paper after the reply rules / drafts. This feeds the open-weight pause gate (more than 10% in any Doer-and-goal cell) |
| `revise_truncated` share | Reviewed runs ended by a cut-off revision / reviewed runs |
| Repeat share | Repeated entries / all returned entries |
| Untitled share | Untitled entries / all returned entries |
| Unreviewed share | Current papers still without a ruling after the repair turn / audited papers |
| Off-list rulings | Auditor rulings on papers outside the current list / audited papers |
| `window_full` share | Open-weight reviewed runs stopped for the token window / reviewed runs |

## 8. Performance (H7)

| Measure | Formula |
| --- | --- |
| Tokens, calls | Prompt and completion tokens, and calls, by role and stage, from the run logs |
| `cost_usd` | Tokens × the dated price file. For the open-weight arm, OpenRouter's reported cost is logged beside it |
| `cost_per_valid_paper` | `cost_usd` / `compliant_count`. Undefined when the count is 0 |
| `working_time_s` | Wall-clock seconds per run. Not measured for Claude runs, which go through the Batch API |
