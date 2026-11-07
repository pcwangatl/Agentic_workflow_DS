# Pre-registration: agent-team set-up and literature-reference errors (Study B1)

**Status.** Design frozen on 6 November 2026. This file is registered in two tagged commits: `prereg-tag1`, before the first paid call of the study (the Lead-plan calls included), and `prereg-tag2`, before the main run. Any change after `prereg-tag1` is a dated amendment listed in [AMENDMENTS.md](AMENDMENTS.md).

**Authors.** Withheld during peer review.

**Code name.** The study is called B1 in the code, configuration and logs.

---

## 1. Summary

The study asks whether the way an AI agent team is set up changes two things when the team works from memory without tools:

- how often it invents or misreports literature references;
- how many usable references it returns.

**The team.** A Lead plans the subtopics, a Doer writes the reference list, and an Auditor checks it.

**What varies:**
- how capable each role is;
- how many papers the team is asked for;
- whether it may report too few;
- what kind of Auditor reviews the list.

**Two arms.** The study has two arms, analysed separately, each with its own verdicts and no pooling:
- an API-hosted arm with four commercial models;
- an open-weight arm with three Qwen models and Gemma Auditors, served through OpenRouter (section 7).

**Earlier runs.** The design was developed on earlier exploratory pilot runs. These are not reported and are not compared with this study. Short tests of the study code were also run before registration, and their data never enter the analysis.

## 2. How one run works

1. **Lead.** The Lead model writes 10 subtopics for a HICSS-59 mini-track. There is one frozen plan per mini-track, vendor and Lead level.
2. **Doer draft.** The Doer lists papers for each subtopic from memory. For each paper it gives the title, authors and year, the journal where the paper actually appeared, and a one-line summary. Only articles in the 34 approved journals, published from 2010 to 2024, count.
3. **Auditor review** (only in cells that have one). The Auditor reads the list and objects to papers it thinks break a rule or do not exist. The Doer then revises. There are at most 3 audit rounds.
4. **Final list.** The final list is saved. Every call's prompt and reply are logged.
5. **After data collection.** The verifier looks up every logged citation, in Crossref first and then OpenAlex, and labels it by the first check it fails. Scripts then build every dependent variable (DV) from those labels and the run logs. No model ever sees a rate or a label.

## 3. Treatments (API-hosted arm)

Five factors vary. Each one varies within the same mini-track, so every comparison is made on the same topics.

| Factor | Levels | Where it acts | Tested by |
| --- | --- | --- | --- |
| Lead capability | Low or high, within the Doer's vendor: Claude Haiku 5.5 or Sonnet 5.5; DeepSeek Flash or V4-Pro | The subtopic plan | H8 |
| Doer | Claude Haiku 5.5, Claude Sonnet 5.5, DeepSeek Flash, DeepSeek V4-Pro: a low and a high model per vendor | The draft and the revisions | H4a |
| Goal | 3 or 10 papers per subtopic, so 30 or 100 papers in all | The draft | H1, H5, H6x |
| Instruction | Must-fill: "return exactly N papers for each subtopic". May-report: return fewer and say the subtopic has too few known papers | The draft | H6, H6x |
| Review | None; same-vendor Auditor at low or high tier (same-L, same-H); other-vendor Auditor at low or high tier (cross-L, cross-H) | The final list, for high-Lead drafts only | H2, H3, H5, H9 |

**Cells per mini-track.** 2 Leads × 4 Doers × 2 goals × 2 instructions = 32 drafts. The 16 low-Lead drafts are not reviewed. Each of the 16 high-Lead drafts runs under all five review levels. That makes 96 cells per mini-track: 32 drafts and 64 reviewed runs.

## 4. What stays fixed

| Element | Setting |
| --- | --- |
| Paper format | The venue field is honest: it gives the journal where the paper actually appeared. There is no on-list flag and no APA line. Only the 34 approved journals count. An off-list paper never counts toward the goal. |
| Wording | These are fixed in the study's prompt file and config, which the hash file names by SHA-256: the must-fill and may-report wording, the revise rules, and the 3-audit cap. Papers still under objection when the cap is reached stay in the list and are flagged. |
| Models and settings | Model IDs are fixed and listed in the config. Thinking is off, set per model: Claude Haiku 5.5, DeepSeek Flash and DeepSeek V4-Pro use `thinking: disabled`. Claude Sonnet 5.5 uses `between_tools`, because its API rejects `disabled`; no tools are given. DeepSeek runs at temperature 0. Claude runs at the provider default, because its API rejects a temperature setting. There is no request seed, because neither API supports one. Review calls have a 131,072-token limit so that they can carry the review history. Claude calls go through the Batch API. |
| Verifier | One frozen version for both the pilot and the main run: verifier version 4 (dated 29 October 2026) plus the venue-matching fix (Appendix B), named by hash at `prereg-tag1`. |
| Lead plans | The study's own plans for every mini-track. They are generated after `prereg-tag1` and before any draft, and each plan file is frozen by its SHA-256 hash before drafting starts; the hashes are listed in the hash file at `prereg-tag2`. The stage-2 format arms reuse the same plans. Drafts are never reused. |
| What each role sees | See "Review history" below. |
| Run order | Mini-tracks run in the drawn order (section 5), in waves of 10. Within each mini-track, every cell runs in a seeded random order (balanced blocks, seed 20261030), so no factor level runs only early or only late. The journal list is always shown in the same order. |

**Review history.** Both the Auditor and the Doer remember the earlier audit rounds.

- **Each call.** Each audit and each revision is a new call. It contains:
  - the Lead's subtopics, the rules, the journal list and the current list;
  - for the revising Doer, that round's objections and reasons.
- **The history block.** Below that comes a history of every earlier round: the Auditor's decision and reason for each citation, and the Doer's disposition, note and any replacement.
- **Round 1.** The history is empty, so the round-1 prompt is the same as a prompt without history.
- **Same history for both.** Both roles see the same history in every review cell.
- **Round numbers.** Rounds are numbered, but the 3-audit cap is not stated.

How the history is built:
- It is built around the current list. Each current paper carries its own earlier rulings.
- A replacement is shown with the title, authors, year and journal of the paper it replaced, the round in which that paper was removed, and the Auditor's ruling and reason. For example: Replaces "Title" (Author, 2009), Journal X, removed in round 1, ruling replace: published outside the window.
- Papers that have left the list get no lines of their own.
- A paper removed without a replacement is listed by title only.
- So no outdated ID appears in the prompt.

How audits are handled:
- The audit instructions say to rule only on the papers in the current list. The runner ignores any ruling on a paper outside the list and logs it.
- If an audit leaves current papers without a ruling, the call's one repair turn asks for rulings on exactly those papers, if no format repair has used that turn.
- Papers still without a ruling stay in the list, are flagged unreviewed, and are counted by cell.
- A reply that cannot be read gets one repair turn that shows it the parse error. A reply cut off at the output limit is the exception (section 11).

## 5. Sample and runs (API-hosted arm)

Mini-tracks are drawn at random from the HICSS-59 mini-track list.

- **Pool.** Every mini-track in the list that no earlier exploratory run or code test used: 89 mini-tracks.
- **Draw.** The pool, sorted by mini-track ID, is shuffled once with Python's `random.Random(20261107).shuffle`.
- **Split.** In the shuffled order, the first 10 are the pilot, the next 50 are the main run's full grid, and the rest, up to 50, are the main run's drafts-only set: 29 mini-tracks with this pool.
- **Record.** The draw script, the pool list and the three resulting lists are named by hash at `prereg-tag1`.

The draw is made before any paid call, so the split works as a random assignment.

| Part | Mini-tracks | What runs | Drafts | Reviewed runs |
| --- | --- | --- | --- | --- |
| Lead plans | All 89 | 4 plans each (2 vendors × 2 Lead levels): 356 Lead calls | — | — |
| Pilot stage 0 | — | Offline checks and a dry run | — | — |
| Pilot stage 1 | 1 pilot mini-track | Full grid, readiness check | 32 | 64 |
| Pilot stage 2 | 10 pilot | High-Lead drafts in three formats: the honest format; the old forced-list format, as a same-time control; and the honest format with the APA line kept | 480 | — |
| Pilot stage 3 | 10 pilot | Full grid in the honest format. All 320 drafts are new: the 160 honest high-Lead drafts are drafted again, not reused from stage 2, and the two copies give the run-to-run tolerance (section 13) | 320 | 640 |
| Main, full grid | 50 drawn | All 96 cells | 1,600 | 3,200 |
| Main, drafts only | 29 drawn | All 32 draft cells, no review | 928 | — |

**Which data test what:**
- Draft hypotheses (H1, H4a, H6, H6x, H8) use all 79 main mini-tracks.
- Review hypotheses (H2, H3, H5, H9) use the 50 full-grid mini-tracks.
- Pilot data never enter the analysis.

**Waves.** Wave 1 is 10 full-grid mini-tracks, so the spend check sees the most expensive runs first. Later waves mix both kinds, so a spend stop leaves both samples usable.

## 6. Hypotheses

**Tests.** Each hypothesis has one primary contrast and one deciding DV, named in advance. H9 is the exception: it is decided on all four primary DVs. The other primary DVs are tested on the same contrast and are reported, with stars, as supporting evidence. All tests are two-sided at raw p < .05, with no adjustment for multiple tests.

**Verdicts:**
- *Supported*: the deciding DV is significant in the predicted direction.
- *Not supported*: the deciding DV is not significant. Failing to reject is an acceptable, reported result.
- *Opposite*: the deciding DV is significant in the other direction.
- *Partly supported*: the deciding DV moves as predicted, but `compliant_count` fails its 10% non-inferiority check. The check fails when the lower end of the 90% interval falls below −10% of the comparison mean. This check applies to every "helps" verdict: H3, H4a, H6 and H8. H2 and H9 already have `compliant_count` among their deciding DVs.

**H9 verdict.** H9 is tested on four DVs, and each result is reported:
- `compliant_count`, predicted to go up;
- `fabrication_rate`, `year_mismatch_rate` and `misplacement_rate`, predicted to go down.

One overall verdict:
- *supported* if at least one DV is significantly better and none is significantly worse;
- *mixed* if some are better and some are worse;
- *opposite* if only worse;
- *not supported* otherwise.

With four tests at raw p, the chance of a false "supported" verdict is roughly 10%, not 5%. The paper states this.

| ID | Prediction | Primary contrast | Data | Deciding DV and test | Status |
| --- | --- | --- | --- | --- | --- |
| H1 | Higher goals raise hallucination | Goal 10 minus goal 3 | Drafts, 79 mini-tracks | `fabrication_rate`, two-sided | Confirmatory |
| H2 | An Auditor improves the list | Any Auditor (the four levels averaged) minus none; each final list is compared with its own draft | Review, 50 | `compliant_count` up | Confirmatory |
| H3 | An other-vendor Auditor lowers fabrication more than a same-vendor one, because a different model family brings more diverse knowledge | Cross minus same, averaged over tiers and vendors | Review, 50 | `fabrication_rate` down, two-sided p < .05. Failing to reject is an acceptable result. `realized_false_rejection` is a named secondary | Confirmatory, directional |
| H4a | A more capable Doer lowers fabrication | High minus low Doer within vendor, averaged over vendors | Drafts, 79 | `fabrication_rate` down | Confirmatory |
| H5 | Review helps most at high goals | (Goal 10 minus 3) × (any Auditor minus none) | Review, 50 | `fabrication_rate` | Secondary |
| H6 | Permission to report too few lowers fabrication without losing valid papers | May-report minus must-fill | Drafts, 79 | `fabrication_rate` down, and `compliant_count` non-inferior to must-fill at a 10% margin. Both: supported. Fabrication only: partly supported | Confirmatory |
| H6x | The H6 effect depends on the goal | (May-report minus must-fill) at goal 10, minus the same at goal 3 | Drafts, 79 | `fabrication_rate` | Secondary |
| H7 | Efficiency: every confirmatory contrast is repeated on cost | As in each hypothesis | As above | Tokens, `cost_usd`, and working time. Time is not measured for Claude runs, which go through the Batch API | Secondary |
| H8 | A more capable Lead lowers fabrication | High minus low Lead within vendor, averaged over vendors | Drafts, 79 | `fabrication_rate` down, two-sided p < .05. Failing to reject is an acceptable result | Confirmatory |
| H9 | A higher-tier Auditor improves overall performance more than a lower-tier one | High minus low tier, averaged over families and vendors | Review, 50 | All four primary DVs, each in the better direction (`compliant_count` up; `fabrication_rate`, `year_mismatch_rate` and `misplacement_rate` down), two-sided p < .05. One overall verdict by the H9 rule above. `realized_false_rejection` is a named secondary | Confirmatory, directional, on all four primary DVs |

## 7. Open-weight arm (OpenRouter)

**Analysed on its own.** The open-weight arm is analysed as its own study, with its own verdicts and no pooling with the API-hosted arm.

**What is the same.** Everything not listed in this section works exactly as in the API-hosted arm:
- the run flow, goals 3 and 10, must-fill and may-report, and review on high-Lead drafts only;
- the 3-audit cap, the review history and the final output rule;
- the paper format, the verifier, the DVs, the hypotheses and the verdict rules;
- the manipulation check, in which each Doer is compared with this arm's own same-time old-format drafts;
- the drawn mini-tracks and their split, the run order, and pilot stages 0 to 3.

| Factor | Open-weight arm |
| --- | --- |
| Lead capability (H8) | Low = Qwen3-14B, high = Qwen3-32B |
| Doer (H4a) | Qwen3-14B, Qwen3-32B, Qwen3.8-27B |
| Review (H2, H3, H5, H9) | None; same-family Qwen3-14B (same-L) or Qwen3-32B (same-H); other-family Gemma 3 12B (cross-L) or Gemma 3 27B (cross-H) |
| Cells per mini-track | 2 Leads × 3 Doers × 2 goals × 2 instructions = 24 drafts, plus 48 reviewed runs (72 in all) |

The low-versus-high contrast is Qwen3-14B against Qwen3-32B, a milder gap than in the API-hosted arm, and the write-up says so.

| Model | Token window / max output | Precision |
| --- | --- | --- |
| Qwen3-14B | 40,960 / 16,384 | fp8 |
| Qwen3-32B | 40,960 / 16,384 | fp8 |
| Qwen3.8-27B | 262,144 / 235,929 | bf16 |
| Gemma 3 12B | 131,072 / 16,384 | bf16 |
| Gemma 3 27B | 131,072 / 16,384 | fp8 |

**Provider.**
- Every model is served by DeepInfra through OpenRouter, pinned to that provider with fallbacks off and zero data retention.
- Prices are taken from a dated price file.
- With one pinned provider, an outage pauses the run; it never switches providers.

**Provider rule.** Any provider chosen for the study, now or as a later replacement, must meet all of these:
- full or near-full precision (no 4-bit weights);
- a reliable uptime record;
- seed support;
- the window the study needs;
- zero data retention.

Price is considered only after those are met. A replacement is recorded as an amendment.

**Thinking off.**
- **Qwen3-14B and Qwen3-32B.** Every prompt, for the Lead, the Doer and the Auditor, ends with "/no\_think". In development tests, no request setting turned these models' thinking off on this provider, and thinking left on could use up the whole output limit. The runner removes the empty think block they return before parsing.
- **Qwen3.8-27B.** This model ignores "/no\_think" on this provider, so its thinking is turned off with OpenRouter's reasoning setting, as fixed in the config. In development tests that setting returned no reasoning tokens. Its prompts carry no "/no\_think" line.
- The "/no\_think" line is the only prompt wording that differs from the API-hosted arm.

**Logging.** Every call logs:
- the served provider (OpenRouter does not report precision for each reply; it is fixed by the pinned endpoint);
- the model ID;
- any reasoning tokens;
- OpenRouter's reported cost.

**Sampling.** Each model uses its own recommended non-thinking settings with a fixed request seed. Greedy decoding can make Qwen models repeat themselves.

| Models | Temperature | Top-p | Top-k |
| --- | --- | --- | --- |
| Qwen3 | 0.7 | 0.8 | 20 |
| Gemma 3 | 1.0 | 0.95 | 64 |
| Qwen3.8-27B | its model card's non-thinking values, as fixed in the config | | |

- Each call gets its own seed, derived from a fixed base seed (20261106).
- No presence penalty is used, for any model, including the one in Qwen3.8-27B's card. It can cause language mixing and lower quality, and it would tune one arm toward a better result.

**Output limits.**
- Every model has the same output limit of 16,384 tokens.
- Each call's `max_tokens` is min(16,384, window − prompt).
- A run whose next audit or revision call would leave fewer than 4,096 tokens for the reply stops there (section 11, final output rule). The room left is estimated from the prompt's length (3 characters per token, plus a 3% and 256-token margin), so a run may stop slightly early, never late.

**Goal 10.** Goal 10 stays in this arm so that it mirrors the API-hosted arm. Repeated, cut-off and untitled entries are treated as outcomes under the rules in section 11, not as faults to tune away. The pilot gate in section 10 decides whether goal 10 holds up.

| Part | Mini-tracks | Drafts | Reviewed runs |
| --- | --- | --- | --- |
| Lead plans | All 89 × 2 Lead levels: 178 Lead calls | — | — |
| Pilot stage 1 | 1 pilot mini-track | 24 | 48 |
| Pilot stage 2 (three formats, 120 each) | 10 pilot | 360 | — |
| Pilot stage 3 | 10 pilot | 240 | 480 |
| Review tolerance repeat (stage 3, run a second time) | 10 pilot | — | 480 |
| Main, full grid | 50 drawn | 1,200 | 2,400 |
| Main, drafts only | 29 drawn | 696 | — |

**Pilot additions in this arm:**
- **Stage 0.** Counts every goal-10 review prompt with each model's own tokenizer, and reports the share that would be trimmed or stopped. Checks every sampling value against the model card.
- **Stage 1.** Checks three things:
  - every reply came from the pinned DeepInfra endpoint;
  - no reasoning tokens were billed for any of the three Qwen models;
  - the sampling settings and seed sent are the planned ones, and DeepInfra applies them.
- **Stages 1 and 3.** Reports the truncated, salvaged, repeat and untitled shares, and the window-full stops, for each Doer and goal.
- **Pause gate.** If more than 10% of the drafts in any Doer-and-goal cell fail outright, with no usable paper, the run pauses. Any change, for example a lower top goal in this arm, is made only as a dated amendment before the main run.

**H4a in this arm.** The primary H4a contrast is Qwen3-32B minus Qwen3-14B, matching the arm's low and high levels. Qwen3.8-27B is a third Doer level; it is reported against both but does not decide H4a.

## 8. Dependent variables

Every DV is computed after data collection, from the logged citations, the verifier labels and the run logs. The formula for each DV is in [docs/dv\_specification.md](docs/dv_specification.md).

**Check order.** Each citation gets the label of the first check it fails, in this order:

1. The paper exists. If not: fabricated.
2. The authors and year are right. If not: misattributed. The year is checked before the journal.
3. The journal is the one the paper appeared in. If not: misplaced.
4. It is an article in one of the 34 approved journals. If not: off-venue, which is a rule break, not a hallucination.
5. The year is in the 2010–2024 window.

| DV | Status | What it counts | Per |
| --- | --- | --- | --- |
| `compliant_count` | Primary; the registered count DV. `valid_count`, which adds a relevance check, is a secondary only if the relevance judge runs | Papers that pass every check | Run |
| `fabrication_rate` | Primary | Papers that do not exist | Resolved unique citations |
| `year_mismatch_rate` | Primary | Real papers whose cited year is off by 2 or more. An author rule joins only if the `title_only` hand check (section 10) says so | Real works |
| `misplacement_rate` | Primary | Real works cited under a journal they never appeared in, including a book, chapter or conference paper given a journal name | Real works |
| `fabricated_count`, `misplaced_count`, `misattributed_count` | Secondary | The same labels, as counts | Run |
| Top-3 versions of the three rates | Secondary | The first 3 papers of each subtopic | As above |
| `author_mismatch_rate` | Secondary | Real works with any cited author missing from the record | Real works |
| `minor_error_rate` | Secondary | The right paper with a small slip, such as a year off by 1 or a title typo | Accurate works |
| Relabel DV | Secondary, if its definition is added by amendment before `prereg-tag2`; otherwise not reported as a registered measure | A rejected paper kept but moved to another journal | Revisions |
| `answer_rate`, `refusal`, `abstention_rate` | Secondary, reported beside every draft contrast | Drafts with at least one resolved citation; refusals; abstained subtopics | Draft; subtopic |
| `realized_false_rejection` | Secondary (H3, H9) | Compliant papers an Auditor wrongly removed | Run |
| Review measures: `review_net_change`, `reviewer_miss_rate`, `reviewer_false_flag_rate`, `correction_success`, `miss_correlation`, replacement rates per type | Secondary | The lineage of each paper from draft to final list | As defined in the DV specification |
| `review_cap_reached`; the final list without papers still under objection | Secondary | Runs that hit the 3-audit cap | Run |
| `abstention_targeting`, `answered_hallucination_gap` | Secondary | Paired must-fill and may-report drafts | Subtopic |
| `venue_violation_rate` | Exploratory, outside the main results | Real works honestly cited under their real off-list venue | Real works |
| `window_violation_rate`, `year_error_rate`, `off_topic_rate`, year-window versions of `valid_count` | Reported, not tested | As defined in the DV specification; `off_topic_rate` only if the relevance judge runs | As defined there |
| `rehomed_rate`, `journal_field_empty_rate` | Manipulation and data checks | Real papers cited under an approved journal they never appeared in; empty Journal fields | Real works; citations |
| Tokens, calls, `cost_usd`, `cost_per_valid_paper`, `working_time_s` | Performance (H7) | Run logs and a dated price file | Run |
| `unresolved_share` | Data quality | Citations the verifier could not settle. Both bounds are reported for every deciding contrast (section 12) | Unique citations |
| Truncated, salvaged, repeat and untitled shares; unreviewed papers; window-full stops | Data quality, reported by cell | Section 11 | Draft or run |

## 9. Manipulation check

The honest venue field should remove re-homing, which means moving a real paper under an approved journal to fit the list. The check is `rehomed_rate`, which the verifier computes for each Doer after data collection.

## 10. Pilot gates

| Step | Gate (must pass to continue) |
| --- | --- |
| Stage 0, offline | Every rendered prompt differs from the old format only where planned. Parser and rendering tests pass. A dry run through a fake API passes. The verifier is unchanged apart from the venue-matching fix. Review-history prompts render as planned: round-1 prompts are identical to prompts without history, the history is built around the current list with no outdated IDs, and the audit prompt carries the current-list-only line. The repair turn for unruled papers works on a fake API. The cut-off, salvage, repeat and untitled rules give the expected results on saved test replies. Every prompt fits the window. |
| Stage 1, readiness | Every reply parses or is a recorded refusal. The served model names match the planned IDs and are logged. Cost per run is within ±30% of the planning estimate. Auditor rulings on papers outside the current list are under 1% of audited papers. Current papers still without a ruling after the repair turn are also under 1%. |
| Stage 2, formats | For every Doer, `rehomed_rate` in the honest format is at most half that of the same-time old-format arm. Against that arm, pooled over the arm's Doers: `fabrication_rate` may be no more than 3 points higher; the refusal rate no more than 5 points higher; the parse rate no more than 2 points worse. Each Doer's own difference is reported beside the pooled one. The APA-kept arm shows whether a leftover rate comes from swaps or from memory errors. |
| Stage 3, full-grid pilot | At most 3% of replacements keep a rejected paper and only move it to another approved journal. The projected main-run cost is under the arm's spending cap. No new failure types appear. The 160 honest high-Lead drafts (120 in the open-weight arm) are drafted again; the stage-2 and stage-3 copies give the run-to-run tolerance (section 13). |
| Hand checks before `prereg-tag2` | Two checks on B1 pilot data must finish before `prereg-tag2`: 100 venue-matching cases, and 100 `title_only` citations. The `title_only` check decides whether an author rule joins `year_mismatch_rate`. A third check, 100 citations coded blind by two coders, validates the verifier and changes no rule, so it can run alongside the main run. |
| Main run | Each Doer's ceiling is the upper end of the 95% interval of its pilot honest-format `rehomed_rate`, from a mini-track cluster bootstrap. The formula is frozen at `prereg-tag1`; the numbers are added at `prereg-tag2`. A Doer above its ceiling stays in the primary verdicts and is flagged, and results without it are a sensitivity check. After the first wave of 10 mini-tracks, a spend projection stops the run if it would pass the arm's spending cap. |

If a gate fails, the pilot stops. Any fix, and any repeated stage, is recorded as a dated amendment before the pilot continues.

## 11. Exclusion and stopping rules

- **Empty drafts.** A draft with no resolved citation has no rate. It is left out of the rate DVs and counts 0 in `compliant_count`. It shows in `answer_rate`, which is reported beside every rate contrast. A reviewed run whose list becomes empty stops reviewing and is treated the same way.
- **Refusals.** A refusal, whether in refusal wording or stopped by the provider's safety filter, is the model's answer:
  - it is recorded, never asked again, and counted in the refusal DV;
  - a refused draft is an empty draft;
  - a refusal during review ends the run with the list as it stands, flagged.
- **Cut-off replies.** A reply cut off at the output limit gets no repair turn.
  - *Cut-off draft:* every complete, well-formed paper before the cut is kept, and the draft is flagged truncated.
  - *Cut-off revision:* the run ends. The Doer's last complete list is the output, flagged `revise_truncated`.
- **Other unreadable replies.** Any other unreadable reply gets one repair turn that shows the parse error.
  - *Draft still unreadable:* its complete, well-formed papers are kept in the same way, and it is flagged salvaged. With none, it is a failed draft and is treated like an empty draft.
  - *Revision still unreadable:* it changes nothing, and the run goes on.
  - Every flag is reported by cell.
- **Repeated papers.** Within one list, a paper whose title matches an earlier paper's title is a repeat. Titles are compared lower-cased, with punctuation and spacing removed. Every DV counts only the first appearance, and the repeat share is reported by cell.
- **Untitled papers.** A paper with no title cannot be checked. It counts 0 in `compliant_count` and is left out of the rate DVs, like an empty slot. The untitled share is reported by cell.
- **Papers with a title only.** A paper with a title but no authors or year goes through the verifier as usual.
- **Both arms.** The cut-off, unreadable, repeat and untitled rules apply to both arms.
- **Server and network errors.** These are retried up to 3 times with backoff, logged, and never scored.
  - A call that still fails ends its draft or run as failed.
  - Failed items are rerun once before analysis, inside the spending cap.
  - Anything still failing is left out and listed in a failure table by cell.
- **Served model.** Every reply's served model is logged; in the open-weight arm, so is its provider.
  - A reply whose served model differs from the ID confirmed in stage 1 is left out, and its item is rerun once.
  - If this happens to more than 1% of calls, collection stops. It resumes only after the cause and any fix are recorded as an amendment.
- **Final output rule.** A team's output is the Doer's last list, and every DV is computed on it.
  - The Auditor's last verdict only sets the pass or cap flag. It never removes a paper or changes the list.
  - A list the Auditor passes is final.
  - If the third audit still objects, the run stops at the 3-audit cap and the Doer's last revision is final. Papers still under objection stay in and are flagged (`review_cap_reached`).
  - A capped run never counts as having no output.
  - Empty lists, refusals, unreadable revisions and failed calls follow the rules above.
  - The secondary list without papers still under objection is computed afterwards from the logged decisions, and is reported beside each review contrast.
  - In the open-weight arm, a run whose next review call cannot fit the model's token window (fewer than 4,096 tokens left for the reply) stops there in the same way. The Doer's last list is the output, flagged `window_full` (logged as `review_window_full` or `revise_window_full`, by the call that would not fit), and the flag is reported by cell.
- **Spend stop.** If the spend projection stops a main run, only complete mini-tracks, with all of their cells finished, are analysed. The shortfall is reported.
- **Pilot data.** No pilot draft or run enters the analysis. The repeated stage-3 drafts and runs are used only for the tolerance.

## 12. Analysis plan

- **Model.** OLS with mini-track fixed effects, with standard errors clustered by mini-track.
- **Draft hypotheses** are estimated on drafts, with the other draft factors as fixed effects.
- **Review hypotheses** compare each final list with its own draft, using draft fixed effects. Reviewer error measures use the first audit round only.
- **Robustness checks:**
  - Poisson models for counts;
  - fractional logit for rates;
  - a mini-track cluster bootstrap with 2,000 resamples;
  - unresolved citations counted first as all valid, then as all hallucinated;
  - the journal-first check order, as a sensitivity table.
- **Margins.** No hypothesis uses an equivalence test; H3, H8 and H9 are directional. The 10% non-inferiority margin on `compliant_count` applies to H6 and to every "helps" verdict (section 6).
- **Reporting.** Tables mark \* p < .05, \*\* p < .01 and \*\*\* p < .001, on raw p.

## 13. Run-to-run tolerance

The models are not fully repeatable. The tolerance answers one question: how large can the difference between two identical runs be and still be ordinary noise?

- **Data.** In pilot stage 3, the honest-format high-Lead drafts are drafted a second time with the same models, prompts, Lead plans and settings: 160 drafts in the API-hosted arm and 120 in the open-weight arm. The stage-2 and stage-3 copies are then compared mini-track by mini-track.
- **Tolerance.** For each Doer and each primary DV, the tolerance is the 95% range of (second copy − first copy) across the 10 pilot mini-tracks.
- **Open-weight review DVs.** The arm's review tolerance repeat, which runs the 480 stage-3 reviewed runs again, gives the same range for the review DVs.
- **Comparison rule for a future replication.** A replication matches this study if each hypothesis' estimate falls inside this study's 95% interval, widened by that run-to-run spread.
- **Timing.** The rule is frozen at `prereg-tag1`. The numbers are added at `prereg-tag2`, before any main-run data exist.

## 14. Registration record

**Frozen at `prereg-tag1`, before the first paid call of the study (the Lead-plan calls included):**
- this document: the hypotheses with their predictions, contrasts, deciding DVs and verdict rules; the DV rules and check order; the exclusion, stopping and gate rules; and the ceiling and tolerance formulas;
- the prompt file and config;
- the models and settings, the verifier version, and the mini-track draw, its lists and the run order;
- the SHA-256 hash of every file that fixes these: the study code (runner, parser, verifier), prompt files, configs, the task file, the mini-track draw script and its lists, the journal lists and the DV code, 62 files in all ([registration/tag1\_hashes.sha256](registration/tag1_hashes.sha256)). The files themselves are published with the replication package, and anyone can check them against these hashes.

**Added at `prereg-tag2`, before the main run:**
- the hashes of the Lead-plan files;
- the pilot-set values: each Doer's `rehomed_rate` ceiling, the `title_only` author-rule decision, and the tolerance numbers;
- each arm's spending cap for the main run;
- the analysis code;
- a hash file (SHA-256) of every frozen file.

## 15. Known limits at registration

- **Review hypotheses in the API-hosted arm.** The run-to-run tolerance covers draft DVs only. There is no repeat of reviewed runs in this arm, so the tolerance for the review hypotheses (H2, H3, H5, H9) is not measured.
- **Prompt wording.** Each condition uses one wording, so sensitivity to prompt wording is not tested.
- **Seeds and sampling.** The API-hosted models take no request seed, and Claude models run at the provider's default sampling.
- **Single provider.** The open-weight arm relies on one pinned provider.

---

## Appendix A. Prompt format

The honest format differs from the old forced-list format, which is used only in the stage-2 control arm, in the places below. Every other block stays byte for byte.

- **Requirement 3, last sentence.**
  - Old: "Give the journal name exactly as it appears in the list."
  - New: "Give the journal where the paper actually appeared, spelled as in the list if it is on the list. Never change a paper's journal to make it fit the list: a real paper given the wrong journal counts as a wrong citation."
- **Paper format.** The `apa` entry is dropped. The stage-2 old-format arm uses the earlier text unchanged, and the APA-kept arm puts the `apa` entry back first. The new format:

  `{"title": "article title", "authors": ["Surname, I. I."], "year": 2020, "journal": "the journal where this paper actually appeared", "summary": "one sentence on what the paper found"}`
- **What the Auditor and the revising Doer see.** `title:` and `authors:` lines in place of the APA line, then `journal: X | year: Y`. The Auditor's instructions are unchanged, except that in the honest format the fields it may correct are exactly the fields of the honest paper format.
- **Open-weight arm.** Every Qwen3-14B and Qwen3-32B prompt ends with "/no\_think" (section 7).

## Appendix B. Code and verifier

- **Parser.** A paper needs a title. Text outside the JSON object is stored, not scored.
- **Verifier.** The verifier-4 gates are unchanged. The venue-matching fix matches cited venue names by ISSN-L and by alternate journal names.
  - A book, proceedings or preprint record cited under its publisher or proceedings name stays off-venue.
  - A non-journal record with no stored venue counts as misplaced when the field names a journal, and as off-venue when it names a publisher or proceedings.
- **DV scripts.** `build_dvs.py`, including `field_kind`, and the `rehomed_rate` step run on the stored labels.
- **Config.** The study config points to the study prompt file, the study's own Lead plans by hash, and the drawn mini-track lists.
