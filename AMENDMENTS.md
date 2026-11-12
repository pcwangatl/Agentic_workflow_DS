# Amendments

Changes to [PREREGISTRATION.md](PREREGISTRATION.md) or to any frozen file made after the `prereg-tag1` tag. Each entry gives:
- the date;
- the section changed;
- what changed and why;
- which study data, if any, existed at that time.

| No. | Date | Section | Change | Reason | Data existing at the time |
| --- | --- | --- | --- | --- | --- |
| 1 | 2026-11-06 (US Eastern) | 11 (Exclusion and stopping rules), 7 (pilot additions); DV specification section 7 | The cut-off rule now applies only to a reply that stops at the output limit and cannot be read. A reply that stops at the limit but holds a complete, readable JSON object is used like any other reply; the text after the object is stored, not scored. Such replies are counted and reported by cell and role as a new data-quality share. No code or hashed file changes. | Pilot stage 1 showed that the registered text and the frozen code differed: the code, as hashed at `prereg-tag1`, already treats a readable reply this way, which matches Appendix B (text outside the JSON object is stored, not scored). The text is brought in line with the code instead of changing the code, so no valid list is thrown away. | Pilot stage 1 only (1 pilot mini-track). Pilot data never enter the analysis. No main-run data existed. |
| 2 | 2026-11-06 (US Eastern) | 2 (How one run works, step 5); DV specification section 2 and section 6 | The verification order is now Crossref, then a frozen local copy of the 34 approved journals' OpenAlex records for 2010–2024 (named by hash and snapshot date), then a live OpenAlex search only for citations still unmatched that name a journal outside the 34, name no journal, or name a poorly indexed approved journal. A citation naming any other approved journal and found in neither of the first two sources is labelled fabricated without a live search, so a real paper that neither source finds and that is cited under an approved journal can be labelled fabricated instead of misplaced, year-mismatched or off-window. The share of fabricated labels set without a live search is reported by cell. In each Doer and format arm, 10% of those citations (rounded up), drawn with seed 20261107 by a short draw script, also get a live search; this check changes no label and reports how many are real papers. No hashed file changes. The frozen verifier already runs this order. The draw script is new: it is named by its SHA-256 in a dated note below this table before the draw is run, and it is published with the replication package. | Read literally, "Crossref first, then OpenAlex" sends every Crossref miss to a paid OpenAlex search, at a cost far above the planned verification budget. The planned budget assumed a local-copy order. The pilot's stage-2 live searches are capped at $8. In pilot stage 1, labelled from Crossref and the local copy alone, Crossref found all 27 re-homed papers (real papers cited under an approved journal but published outside the 34). The local copy was built from an approved-journal list with SHA-256 64597fa73b2614bfa7ec1a94e8a5b637ea6f87503b337439f7c670f0c8344565. It differs from the list hashed at `prereg-tag1` only in two comment lines, and both hold the same 34 journals. | Pilot stage 1 (1 pilot mini-track), labelled from Crossref and the local copy only, with no live search; pilot stage 2 drafts, collected but not yet verified. Pilot data never enter the analysis. No main-run data existed. |
| 3 | 2026-11-07 (US Eastern) | 2 (step 2), 4 (paper format; Lead plans), 5 (pilot table), 7 (what is the same; pilot table), 9, 10 (stages 0, 2, 2b and 3; main-run ceiling), 13, 14, 15, Appendices A and B; DV specification sections 6 and 7 | The study's paper format becomes the honest-option format, and a new pilot stage 2b tests it before stage 3. Both stage-2b formats give each paper as separate fields (title, authors, year, journal, summary) with no full-reference entry. The control keeps the old forced-list rule: the journal must be one of the 34, written as listed. The honest-option format adds one clause, which lets the Doer return a real paper from another journal, under its real journal, when it cannot recall enough real papers from the approved journals, and one true/false field, `honest_option`, that marks such a paper. The field is a self-report: it never sets a label or a DV, and its shares are reported beside `rehomed_rate`. Stage 2b drafts the 160 high-Lead drafts (120 in the open-weight arm) in each format at the same time, with the stage-2 Lead plans, and is verified as stage 2 was, including the 10% check. The stage-2 gate applies unchanged, with the stage-2b control in place of the old-format arm. Stage 3, the tolerance copies and the main-run ceiling use the honest-option format. Stage-2b spending is capped at $6.00 in all: $1.90 API-hosted, $0.70 open-weight and $3.40 of live searches. Hashed files: two prompt files and six configs are added, and the parser, ledger, prompt builder, workflow, config script and DV script change so that the field is kept, shown to reviewers and counted. The existing prompt files and configs are unchanged. [registration/amendment3\_hashes.sha256](registration/amendment3_hashes.sha256) lists all 70 hashed files. | Pilot stage 2 (7 November 2026) failed its gate. Pooled over the API-hosted Doers, `fabrication_rate` was 91.3% in the honest format against 17.4% in the old forced-list arm, where the limit was 3 points higher. In the open-weight arm it was 99.97% against 89.0%. Re-homing was halved for three of the four API-hosted Doers. The arm that kept the full-reference entry with the honest venue field had 11.3% and passed every gate line, so the rise came from dropping that entry. The study team chose a format without the full-reference entry, and to test an explicit honest option against a same-time control that also has no such entry. | Lead plans for the 10 pilot mini-tracks; pilot stage 1 (1 mini-track, both arms); pilot stage 2 (480 API-hosted and 360 open-weight drafts in three formats), its verification and its 10% check. No stage-2b, stage-3 or main-run data. |
| 4 | 2026-11-07 (US Eastern) | 4 (Lead plans; how audits are handled), 5 (pilot tables), 10 (stage 2b; main run), 14, 15, Appendices A and B | Pilot stage 2b failed its gate in both arms. In the API-hosted arm, the pooled lines passed: `fabrication_rate` was 87.5% in the honest-option format against 94.2% in the control, refusal 1.9% against 4.4%, and parse 100% in both. Re-homing was lower for all four Doers and was halved for Claude Haiku 5.5 (3 of 31 real works, 9.7%, against 3 of 14, 21.4%) and Claude Sonnet 5.5 (4 of 295, 1.4%, against 6 of 65, 9.2%). It was not halved for DeepSeek Flash (14 of 125, 11.2%, against 4 of 25, 16.0%) or DeepSeek V4-Pro (13 of 168, 7.7%, against 14 of 92, 15.2%, where half is 7.6%). In the open-weight arm, almost every paper was invented in both formats (99.89% against 99.91%; 4 real papers of 3,692 against 3 of 3,435), and no draft held a compliant paper. Re-homing rested on 0 to 3 real papers per Doer, so it could not be compared, and that arm's halving line failed. The 10% live-search check found no real paper among 1,106 sampled misses, so no full search was needed. The honest-option format stays the study format in both arms. This amendment makes no other change to the open-weight arm. Whether its stage 3 and main run go ahead is decided and recorded before they run. DeepSeek Flash and DeepSeek V4-Pro are flagged. They stay in every primary verdict, and every verdict is also reported without them, as section 10 already does for a Doer above its ceiling. In the honest-option format, the Auditor's instructions gain one paragraph on papers marked `honest_option: true`, and the revising Doer's replacement line names the "However" rule (Appendix A). The Doer's draft prompt and the control format are unchanged. Before stage 3, a review check runs once on the stage-2b drafts. The 157 answered honest-option high-Lead API-hosted drafts each go through the full review under the new wording, with the other vendor's high-tier Auditor. No new drafts are made. Its data never enter the analysis. It reports the Auditor's rulings on papers whose labels are already known, and the final lists against their drafts. API-hosted spending is capped at $26.00 and live searches at 2,500 searches, which cost $2.50, so the check costs $28.50 at most; the expected spend is about $11–16.50. Hashed files: the honest-option prompt file changes. The runner gains `--drafts-prompt-file`, so that a review can reuse drafts made under an earlier prompt file only when that file has the source run's hash and gives an identical Doer draft prompt. The prompt code gains the hash this check uses. [registration/amendment4\_hashes.sha256](registration/amendment4_hashes.sha256) lists all 70 hashed files; three changed. The code commit is 37832fb95c2ec3a6038886c6c46ca1477a1a11bb. | Stage 2b drafted lists without any review, so it could not show how the Auditor treats a paper marked `honest_option: true`. A check of the registered Auditor prompt found that it never said. The Auditor reads requirement 3 as written for the Doer, where a paper in another journal "does not count", so it could remove a real paper from another journal. It could also take the mark as a sign that a paper is real. The new paragraph keeps the existing bar for every paper: a paper the Auditor believes is made up is removed, whatever its mark. The honest-option format was kept because, in the API-hosted arm, it was as good as or better than the control on every pooled line and lowered re-homing for every Doer. It also gave three times as many real papers per answered draft (3.94 against 1.28) and twice as many compliant ones (0.66 against 0.33). The two halving failures rest on few papers: Flash's control rate comes from 4 re-homed papers of 25 (mini-track bootstrap 95% interval 0–46.2%), and V4-Pro missed half by 0.1 point. In the open-weight arm the two formats did not differ. | Lead plans for the 10 pilot mini-tracks; pilot stages 1, 2 and 2b (drafts, labels and the 10% checks). No list had yet been reviewed in the honest-option format. No stage-3 or main-run data. |
| 5 | 2026-11-08 (US Eastern) | Status line, 2 (step 5), 7 (open-weight arm), 10 (stage 3; hand checks), 11 (cut-off and unreadable replies), 13, 14, 15, Appendix B; DV specification sections 2, 6 and 7 | **Stage-3 result.** Pilot stage 3 ran on 7 and 8 November 2026. In the API-hosted arm, 115 of 16,533 replacements (0.70%) only moved a rejected paper to another approved journal, and no new failure type appeared, so the first and third lines of its gate passed; its cost line is settled when the main-run cap is set at `prereg-tag2`. In the open-weight arm the first line failed: 393 of 7,963 replacements (4.9%), and 3.5% in the review tolerance repeat. **Open-weight arm.** The arm becomes an exploratory boundary-condition check. It tests no hypothesis and has no verdict, gate, p-value or pooled estimate. In the main run it runs the full grid on the 50 full-grid mini-tracks (1,200 drafts and 2,400 reviewed runs), with the registered models, settings, prompts and run order, and it does not run the 29 drafts-only mini-tracks. Every registered DV is reported for every cell, with mini-track cluster-bootstrap 95% intervals, in a section of its own after the confirmatory results. Its citations are labelled from Crossref and the local copy alone, with no live search. Its spending has its own ledger and cap, set at `prereg-tag2`, and a spend stop in this arm does not affect the API-hosted arm. **Live searches.** A citation that names a journal outside the 34 or no journal, and that Crossref and the local copy do not find, is labelled fabricated without a live search, as approved-journal misses already are. The four poorly indexed approved journals keep the live search. The 10% check of amendment no. 2 is widened to these citations. It is drawn within each Doer, each list type (citations that appear in a draft; citations that first appear in a revision) and each kind of miss (approved journal; other or no journal), with seed 20261107, by a draw script named by its SHA-256 in a dated note before the draw. If more than 3% of the drawn citations of the second kind in a Doer and list type are real works, every such citation in that Doer and list type gets the live search and its label. The check of approved-journal misses changes no label, as before. **Near misses.** The verifier and its stored labels are unchanged; the analysis code applies these rules on top of them. A citation with a fuzzy title (similarity 0.80 to 0.90) or a short title counts as a real work with a minor title error when a cited author is on the matched record, and then goes through checks 2 to 5; with no cited author on the record it is fabricated. Each of these two branches is used only if a person agrees with it in at least 45 of 50 pilot cases; a branch that fails leaves its citations unresolved. The `title_only` check adds the author rule only if at least 90 of its 100 citations are real works cited with wrong authors. A citation to a poorly indexed approved journal that no source finds stays unresolved. A citation whose journal name the verifier marks uncertain keeps the verifier's label. **Hand checks and a new tag.** The registered hand checks on pilot data no longer have to finish before the main run. They must finish before a new tag, `prereg-tag2b`, cut after the main run's data collection and before any main-run citation is labelled or any main-run DV is computed. `prereg-tag2` still comes before the main run and freezes the Lead plans, the ceilings, the tolerance numbers, the caps and the analysis code, with every possible hand-check outcome built in. `prereg-tag2b` records the hand-check results, the decisions they set by the bars above, and the SHA-256 of every main-run output file. A third hand check joins the two registered ones: 100 stage-3 API-hosted citations with a fuzzy or short title, 50 with a cited author on the record and 50 without, drawn with seed 20261107 by a draw script named by its SHA-256 in a dated note before the draw. After the main run, a person checks 100 citations decided by the near-miss rule, 50 per branch, and the agreement is reported; this changes no label. **Auditor replies.** An Auditor reply cut off at the output limit, or still unreadable after its repair turn, ends the run, and the Doer's current list is the output, flagged `review_truncated` or `review_parse_error`. This matches the frozen code. No hashed file changes. | The open-weight arm failed a stage-3 gate line twice, and the Doer behind the failure changed between the two runs (Qwen3-14B at 10.1%, then Qwen3.8-27B at 7.5%), so dropping one Doer would not fix it. In stages 2b and 3, 99.6–99.9% of its papers were invented and no list held a compliant paper, so its contrasts on `compliant_count` cannot move and its fabrication contrasts sit at the ceiling. A fix would mean tuning a treatment after seeing pilot data. In the pilot's paid label searches, 131 of 8,230 API-hosted citations (1.59%) and 2 of 2,441 open-weight citations (0.08%) were real works. Labelling these citations fabricated without a search therefore overstates `fabrication_rate` by about 0.6 points in the API-hosted arm, and the widened check measures this in the main data. A real paper in one of the four poorly indexed journals can be compliant, so their labels do not change. In stage 3, 2,804 of 16,447 API-hosted citations (17%) went to adjudication, which scales to about 26,000 cases in the main run, far more than people can decide one by one. Left unresolved, their share of final lists ranged from 3.2% to 29.1% across cells and was lowest under Sonnet Auditors, so the two bounds of the Auditor contrasts (H3, H9) could differ by up to about 25 points. The near-miss rule is the registered real-work test (a title match and a cited author) with the title bar lowered from 0.90 to 0.80 when an author matches. In stage 3 the fuzzy titles split 264 with a cited author on the record and 1,396 without. Moving the hand checks after data collection takes them off the main run's critical path. They use pilot data only, the bars that turn their results into decisions are fixed here, and no main-run citation is labelled until the results are recorded, so no main-run result can inform them. Three exits appeared for the first time in stage 3: `review_refusal` once, `review_truncated` three times and `review_parse_error` twice. The frozen code and the final output rule handle them, but section 11 named cut-off and unreadable replies only for drafts and revisions. | Lead plans for the 10 pilot mini-tracks; pilot stages 1, 2, 2b and 3, with their labels, their 10% checks and the open-weight review tolerance repeat; the amendment-4 review check. Pilot data never enter the analysis. No main-run data existed. |

**Note to amendment no. 2 (2026-11-06, US Eastern).** The draw script for the 10% live-search check is `sample_openalex.py`, SHA-256 `c235d677b0d9a094aebe9bba0da9ff40f1b5ddc2e20f92710d4280fea1ce8921`. It was fixed before the draw was run and is published with the replication package. The $8 cap on the pilot's stage-2 live searches covers both the searches in step 3 and the check.

**Note to amendment no. 3 (2026-11-07, US Eastern).** The stage-2b spending limits are enforced by the runner's spend ledgers, which reserve each call's worst-case cost (the full prompt plus the full output allowance) before the call is sent and settle the real cost afterwards. At $1.90 (API-hosted) and $0.70 (open-weight), the first calls' reservations filled both ledgers within seconds, so many cells stopped with a spending-cap refusal before drafting. The stage-2b spending cap therefore becomes $8.10 in all: $3.50 API-hosted, $1.20 open-weight and $3.40 of live searches. The expected spend is unchanged, about $5.40. When the change was made, these drafts existed: open-weight control 120 of 120, open-weight honest-option 117 of 120, DeepSeek honest-option 80 of 80, DeepSeek control 31 of 80, Claude control 0 of 80, and Claude honest-option still drafting. Drafts already made are kept. The cells refused for the spending cap are run again on the same day with the same configs, prompts and Lead plans, so both formats are still drafted at the same time. No hashed file changes.

**Second note to amendment no. 3 (2026-11-07, US Eastern).** The live-search cap of 3,400 searches ($3.40) for stage 2b, which covers both the labels and the 10% check, is too small. Under the route of amendment no. 2, a citation gets a live search when it has no real or near match and names a journal off the list, names no journal, or names a poorly indexed approved journal. The honest-option format names off-list journals far more often. In the Claude drafts, the labels needed 883 live searches for 2,075 distinct citations in the honest-option format, against 193 for 1,174 in the control. The projected need is 4,500–5,100 searches. The live-search cap becomes 5,200 ($5.20), so the stage-2b spending cap becomes $9.90 in all: $3.50 API-hosted, $1.20 open-weight and $5.20 of live searches. The search route, the labels and the 10% check are unchanged. When the change was made, labelling was under way, and the counts above come from it. No hashed file changes.

**Note on pilot stage 3 (2026-11-07, US Eastern).** Pilot stage 3 runs as registered in both arms (sections 5, 7, 10 and 13), with no change to the plan. It uses the honest-option format with the amendment-4 wording, from code commit 37832fb. In the API-hosted arm it makes 320 new drafts and 640 reviewed runs. In the open-weight arm it makes 240 new drafts and 480 reviewed runs, and then the registered review tolerance repeat runs those 480 reviewed runs a second time. The honest-option high-Lead drafts, 160 in the API-hosted arm and 120 in the open-weight arm, are drafted again and not reused from stage 2b, as section 13 requires. The verifier, the order of checks and the 10% live-search check are those of amendment no. 2. Spending is capped by the runner's ledgers, which reserve each call's worst-case cost before it is sent and settle the real cost afterwards. The caps are $50.00 API-hosted, with about $28–34 expected; $5.00 open-weight, with about $2.50–3.50 expected, the review tolerance repeat included; and 9,000 live searches, costing $9.00, for the labels and the 10% check, with about 7,000–8,500 expected. That is $64.00 at most, with about $38–46 expected. The stage-3 gates in section 10 apply unchanged. These caps do not set the main-run caps, which are added at `prereg-tag2`. No hashed file changes. When this note was written, these data existed: the Lead plans for the 10 pilot mini-tracks; pilot stages 1, 2 and 2b; and the amendment-4 review check. No stage-3 or main-run data existed.

**Addendum to the note on pilot stage 3 (2026-11-07, US Eastern).** The stage-3 caps are rebalanced, and their total stays $64.00 at most. $1.00 moves from the API-hosted ledger to the open-weight ledger, so the caps become $49.00 API-hosted, with about $28–34 still expected, and $6.00 open-weight. The 9,000 live searches, costing $9.00, are unchanged. The reason is the measured open-weight cost. The 240 open-weight drafts cost about $0.84, and a reviewed run costs about $0.0037, so the open-weight arm, the registered review tolerance repeat included, is now expected to cost about $4.30–5.10, against the $2.50–3.50 the note expected. Under a $5.00 cap, the ledger's worst-case reservations could have stopped the last runs of the repeat, so the runner held the repeat until this change was recorded. About $39–48 is now expected in all. Nothing else in stage 3 changes, and no hashed file changes. When this addendum was written, at 10:00 PM US Eastern, pilot stage 3 was under way. In the open-weight arm, all 240 drafts and their 240 runs without review existed, with 472 of the 480 reviewed runs; the review tolerance repeat had not started. In the API-hosted arm, all 320 drafts existed, 11 of them refused, with their 320 runs without review and 158 of the 640 reviewed runs. No stage-3 labels, gate results or main-run data existed.

**Note to amendment no. 5 (2026-11-08, US Eastern).** The draw script for the hand checks before `prereg-tag2b` is `draw_handchecks.py`, SHA-256 `33bfef83a7e74e9256e88c103e8ff7f0815435361fed2d5ddc3b9adcae0fa8d5`. It was fixed before the draw was run and is published with the replication package. From the 16,447 unique citations of the stage-3 API-hosted runs it draws, with one `random.Random(20261107)` and no citation drawn twice: 50 near-miss citations with a cited author on the matched record and 50 without; 100 `title_only` citations; and 100 venue-matching cases. The venue-matching cases are 40 that the verifier judged the same journal by ISSN-L or an alternate name (all 17 such matches to an approved journal and 23 of the 298 to journals off the list), 40 it judged a different journal, and 20 whose journal name it marked uncertain. Within each check, half the cases go to each of the two coders, and the coding sheets show neither the verifier's label, the rule's prediction, the Doer nor the cell.

**Note at `prereg-tag2` (2026-11-08, US Eastern).** This commit adds what section 14 lists for `prereg-tag2`, before the main run. No frozen file changes, and the registered design does not change.

*Lead plans.* [registration/lead\_plan\_hashes.sha256](registration/lead_plan_hashes.sha256) lists the SHA-256 of the six Lead-plan files, one per arm and vendor lane. They hold 476 plans: 60 for the 10 pilot mini-tracks (20 Claude, 20 DeepSeek and 20 open-weight), and for the main run 158 Claude and 158 DeepSeek plans for the 79 API-hosted mini-tracks and 100 open-weight plans for the 50 full-grid mini-tracks. No plans exist for the 29 open-weight drafts-only mini-tracks, which do not run (amendment no. 5). The main-run plans were made on 8 November 2026 from code commit 37832fb, with the pilot's plan prompt (SHA-256 `8931c853a1b2630f9165c4ebfd5b850b30c63a8ce089b80b161600687e9d366f` in all six files), models, settings and seed rule. They cost $0.69 under a $4.00 cap: $0.67 API-hosted and $0.02 open-weight. Two driver scripts made them. `run_main_plans.sh` (SHA-256 `9fafff55f3964a31619ceb1695b09e86839fdd763dc092ba6568986f65c5871b`) made the 158 Claude plans through the Batch API. It then stopped before its DeepSeek lane at the runner's clean-tree check, because the analysis code below had been added to the checkout, uncommitted. The analysis code was set aside, and `run_main_plans_rest.sh` (SHA-256 `d0a75facf6f939d687a68e48f6685d21c787910d3f552277a1f6ed20e48ae81f`) made the DeepSeek and open-weight plans on the clean commit, with the same commands, ledgers and caps. The Claude lane started on a clean checkout. Its 158 requests went to the Batch API in five batches: the first at 17:53 UTC, and the other four between 19:01 and 19:09 UTC, after the analysis code had entered the checkout. The lane's closing provenance records that state (diff SHA-256 `c2172814746014b693bd56fe136d924da3c877652dbf52f5a0a29ffab351fd37`, which is exactly the analysis code). The driver had loaded its code at the start, and no run code reads the analysis files. Rebuilt offline from the clean commit, all 158 Claude requests have the same system prompt, user turns and output limit as the requests sent.

*Analysis code.* Code commit 6069c884ed1fc7c846400bac8ad7f578db79d966 adds the analysis code (version b1-analysis-2; labelling rules b1-am5-rules-1):
- `study_b1/dv/apply_label_rules.py` applies the labelling rules of amendment no. 5 on top of the verifier's stored labels;
- `study_b1/dv/build_dvs_b1_rules.py` runs the frozen DV code on those labels;
- `study_b1/dv/secondary_dvs_b1.py` computes the secondary DVs;
- `study_b1/analysis/analysis_b1.py` and `study_b1/analysis/b1stats.py` fit the section-12 models and give the verdicts;
- `study_b1/analysis/tag2_values.py` computes the values below.

`study_b1/write_hashes.py` now also hashes the analysis directory. [registration/tag2\_hashes.sha256](registration/tag2_hashes.sha256) lists all 76 hashed files: the 70 of amendment no. 4, unchanged, and the six new code files. The hand-check decisions file `study_b1/dv/handcheck_decisions.yaml` holds no results (SHA-256 `d9d121a6e0e17ae15a4fae34fff591c451f29d50a15fc1cc5301b53f6596aed7`). The code refuses to label until the file is filled at `prereg-tag2b`, which records the filled version's hash, so the file is not in the frozen list and every hand-check outcome is built in.

The code fixes these choices:
- **Data.** A draft is the final list of its no-review run. Refused and empty drafts are kept. Failed runs are left out and listed. Only complete mini-tracks are analysed.
- **Models.** Models D1 and D2 use the drafts, with mini-track fixed effects. Models R1 and R2 use the five lists of each high-Lead draft, with draft fixed effects and a dummy for each review level and Doer vendor.
- **Tests.** Standard errors are CR1, clustered by mini-track, with t on G − 1 degrees of freedom. The non-inferiority check uses the 90% interval.
- **Robustness.** The Poisson model keeps the OLS fixed effects. The fractional logit uses mini-track fixed effects with the draft factors. The cluster bootstrap uses 2,000 resamples with seed 20261107.
- **Labelling rules.** The near-miss branch is set by the verifier's top candidate. The author rule counts as `year_mismatch`.
- **Named secondaries.** They are reported without verdicts: `realized_false_rejection` for H3 and H9; H2, H3, H5 and H9 on the list without open objections; and H7 on cost, tokens, calls, cost per valid paper and working time. Measures that exist only for reviewed runs use same-L as the reference, so their H3 and H9 contrasts are estimable and their H2 and H5 contrasts are not. Working time counts only for runs with no Batch model as Doer or Auditor.

*Ceilings and tolerance.* [registration/tag2\_values.md](registration/tag2_values.md) (SHA-256 `7011229df53b8d6e170553557284181464c91c3969c1e9b730b89f34d76d0754`) and its machine-readable copy [registration/tag2\_values.json](registration/tag2_values.json) (SHA-256 `9f34f529e2a151cea8212d6079d423744b9bc15e7907bc1a36f0513b1444a8f2`) cover each of the eight possible hand-check outcomes. For each outcome they give:
- each API-hosted Doer's `rehomed_rate` ceiling (section 10);
- the API-hosted tolerance (section 13);
- the open-weight tolerance, which is descriptive;
- the stage-3 unresolved share.

The analysis code reads the JSON copy. It was computed with Python 3.14; Python before 3.12 changes the last digit of a few values. `prereg-tag2b` picks the row that the hand-check results select. The pilot labels behind these values follow the main run's route under amendment no. 5: Crossref and the local copy, the off-list default label, and the stored live-search answers for misses under the four poorly indexed journals. When both near-miss branches and the author rule apply, the stage-3 unresolved share is 0.6%, against 13.1% when none applies, and the ceilings are:

| Doer | Ceiling |
| --- | --- |
| Claude Haiku 5.5 | 0.353 |
| Claude Sonnet 5.5 | 0.098 |
| DeepSeek Flash | 0.304 |
| DeepSeek V4-Pro | 0.294 |

*Caps.* The two run caps each allow 50% over the expected cost:
- **API-hosted main run:** $225.00, with about $150 expected.
- **Open-weight exploratory run:** $22.50, with about $15 expected.

Live searches are capped at 23,000 searches, costing $23.00, for the main-run labels and the widened 10% check. About 9,400 searches are expected. The cap covers the worst case of the 3% trigger of amendment no. 5, about 19,400 searches. The ledgers reserve each call's worst-case cost before it is sent, as in the pilot. After the first wave of 10 mini-tracks, the spend projection of section 10 applies to each arm.

*Hand checks and the main-run 10% draw.* The draw script of amendment no. 5 wrote the hand-check key in draw order (SHA-256 `3a6cc39e540a1b5fd202a30dfcffd1060c4f905c7700451445a92571aa248885`). `shuffle_handchecks.py` (SHA-256 `95a4408d45f75923b57f9c59033c2308c0cfd7e74ce3bbecb4f555dd58ed840d`), with seed 20261107, then reordered and renumbered the cases within each check, so neither row position nor case ID shows the stratum. Each coder keeps the same cases. The final key has SHA-256 `b951672952e29d08f7c085b4e0d0994cb5bcef1c136a0cc1f471c1b4152d38b6`, and the six final coding sheets are listed below. When this note was written, the sheets and the key were held unsent. The sheets go to the two coders after the `prereg-tag2` release.

The main-run 10% draw script is `sample_openalex_main.py`, SHA-256 `382cdab2736862adff17adf3e8261ea0e713adb9af580cf8688594e8743eaa74`. It runs only after `prereg-tag2b`, on a fresh verification cache. A drawn citation whose Doer and list type the check does not trigger keeps the default label, because the check changes no label used for a DV (section 2, step 5).

| Coding sheet | SHA-256 |
| --- | --- |
| Near miss, PC | `b492cf3151ec32ccdf8211ddc119ab87d0bd906761b33d42f1324f7e1845e267` |
| Near miss, Rain | `cc37243332eb7241335a86e00b9448ffbe905e84e8520e8696a0153f2a15c4cb` |
| `title_only`, PC | `68c1b6bbcdba3773f8c6262ce7234d118250a679f56c4a4efe9b6689172b4c34` |
| `title_only`, Rain | `69fba3e75114deecb0d25462db336cd482f9dcfbeb02f75b6f0ecaab5c84a77d` |
| Venue, PC | `fa1dc70ed9ac6b60a22658d3e130ef53be7eb6b28a5d9e25bd59932a025a1066` |
| Venue, Rain | `925797100820079fefb39111ead20e54e7c5a93ad170bd45beeaf2c9bca40a0f` |

When this note was written, these data existed:
- the Lead plans for the 10 pilot mini-tracks and the main-run mini-tracks;
- pilot stages 1, 2, 2b and 3, with their labels, their 10% checks and the open-weight review tolerance repeat;
- the amendment-4 review check;
- the hand-check sheets and key.

No main-run drafts or other main-run data existed.

**Note at `prereg-tag2b` (2026-11-11, US Eastern).** This commit adds what section 14 lists for `prereg-tag2b`. It comes after the main run's data collection and before any main-run citation is labelled or any main-run DV is computed. No frozen file changes, and the registered design does not change. Times are UTC.

*Main run.* The main run used code commit 6069c884ed1fc7c846400bac8ad7f578db79d966, on a clean tree throughout, under `prereg-tag2` (2e116bfe050da37887569f4a5f0fa6ddcff46e88). It ran from 19:36 on 8 November to 17:59 on 9 November 2026, in eight waves.
- **Waves.** Wave 1 was lines 1–10 of `study_b1/minitracks_main_full_grid.txt`. Waves 2 to 8 dealt the remaining mini-tracks out in drawn order and in proportion:
  - waves 2 to 7 each took six full-grid mini-tracks (lines 11–46) and four drafts-only mini-tracks (lines 1–24 of `study_b1/minitracks_main_drafts_only.txt`);
  - wave 8 took full-grid lines 47–50 and drafts-only lines 25–29.

  The open-weight arm ran each wave's full-grid mini-tracks only. Each wave's list is a file in the main-run file list below.
- **Starting each wave.** Each wave after the first started on its own only if:
  - the previous wave's lanes had ended cleanly;
  - served-model mismatches were at most 1% of calls;
  - the next wave's expected cost, plus one round of ledger reservations, fitted under the arm's cap.

  Each arm was checked on its own ledger, and every check is logged with its numbers.
- **Spend projection.** The projection of section 10 after wave 1 used a formula fixed before the wave-1 numbers were in. Spend so far was added to the wave-1 cost per full-grid mini-track times 40, plus the wave-1 draft-lane cost per mini-track times 29, which is the cost of a drafts-only mini-track. It gave $134.45 against the API-hosted cap of $225.00 (25.30 + 101.21 + 7.94) and $16.38 against the open-weight cap of $22.50 (3.276 + 13.106). Both passed.
- **Concurrency.** The Claude lanes ran with `--concurrency 16` in wave 1 and 64 in waves 2 to 8, to cut the number of Batch rounds. The DeepSeek and open-weight lanes ran with 16 throughout. This is a command-line setting. No hashed file changed, and the seeded cell order is the same.
- **DeepSeek peak hours.** Lanes that call DeepSeek were paused (SIGSTOP) from 5 minutes before each weekday peak window (01:00–04:00 and 06:00–10:00) until it ended. Two pauses ran on 9 November: 00:55–04:00 and 05:55–10:00, both in wave 1's review lanes.
  - Of 7,216 DeepSeek calls, none started inside a peak window.
  - No run in any lane ended on the task deadline.
  - All 284 runs that finished after a pause began have a Claude Doer or Auditor, so they carry no working time (H7).
  - The open-weight lanes were never paused.

| Arm | Mini-tracks | Runs | Outcomes | Calls | Spend |
| --- | --- | --- | --- | --- | --- |
| API-hosted, Claude Doers | 79 (50 full grid, 29 drafts only) | 2,864 of 2,864 | 2,025 success, 97 refused, 742 forced exit | 7,240 | $139.95 of $225.00, both API-hosted vendors |
| API-hosted, DeepSeek Doers | the same 79 | 2,864 of 2,864 | 2,006 success, 51 refused, 807 forced exit | 7,388 | in the line above |
| Open-weight, exploratory | 50 full grid | 3,600 of 3,600 | 3,151 success, 449 forced exit | 5,780 | $15.77 of $22.50 |

Every mini-track has all of its planned runs, and no failed run remains (see below). None of the 20,408 calls had a served model other than the planned one. The log check found no problem in the API-hosted run directories. In the open-weight directories it flags only Qwen3-14B and Qwen3-32B replies that carry a one-token empty thinking block, as in pilot stage 3. The Lead plans of the tag-2 note cost $0.67 API-hosted and $0.02 open-weight, on their own ledgers.

*Main-run files.* [registration/main\_run\_files.sha256](registration/main_run_files.sha256) lists the SHA-256 of every main-run output file: 553 files, and the list's own SHA-256 is `1c5f41be136c49df2e3ced90f5ac5aa99e364d396686acbcf3a5c0e55f2645a1`. It was recomputed at 02:06 on 12 November, after the code commit below, by `hash_main_run.sh` (SHA-256 `ce48ac2f21c755b5d854d738a0ddaabcea9bfe14f04832f20e412c2811f8f9ea`), with the same result as before the commit. The files are hashed exactly as collected. Local paths inside the run configurations, provenance records and invocation logs are left as they are. The replication package replaces them with a neutral root and gives a table of hashes before and after.

*Crossref lookups before this tag.* The frozen verifier's fetch-only mode filled a Crossref cache before this tag (`labels --prefetch crossref`, `src/agentic_workflow/verify/cli.py` SHA-256 `bc9823ee13f1f8dc89af8248511bb32b730d30c8e38e93644c09374aa0a5d271`, code 6069c884 on a clean tree, default pacing). This mode writes no label. It ran from 18:12 on 9 November to 17:12 on 10 November 2026, in 24 passes, one run directory each, one at a time, after the main run had ended.
- **Coverage.** It covered 159,611 citations: 108,929 API-hosted and 50,682 open-weight. Every one was cached, none had no title, and no source error occurred. It made 146,266 requests, 379 of them rate-limited and retried.
- **Nothing computed.** No label, match, similarity score or DV was computed, and no cached answer was read. The verifier's 24 output directories are empty, so no main-run verification output exists before this tag (section 14); the cache holds only Crossref's answers.
- **The cache at this tag.** It is a new cache holding 145,687 files, all Crossref answers and none from OpenAlex. Its sorted manifest of file hashes is [registration/main\_crossref\_cache\_manifest.sha256.gz](registration/main_crossref_cache_manifest.sha256.gz). The file is gzip-compressed, and the unpacked manifest's SHA-256 is `7c530afd3c567aeadfd4aad056c0b3ad7e9021af9f22a5524a831bdc5ddcd9a2`. It was recomputed at 02:06 on 12 November and is byte-identical to the manifest made when the prefetch ended.
- **Dating.** The label pass answers from this cache, so the Crossref answers date from 9 and 10 November 2026.

*Failed items.* Server errors that still failed after the 3 registered retries occurred only in the open-weight arm. They were HTTP 429 replies from the provider to the burst of Qwen3-32B draft calls at the start of a wave. Section 11's single rerun ran right after each wave ended, with the same code, configuration and concurrency, and each item had one rerun only.
- **Counts.** 18 failed rows: 1 in wave 4 and 17 in wave 5. All 18 were rerun once: 16 ended in success, and 2 ended as forced exits (`review_truncated`). The API-hosted arm had no failed item.
- **One run kept as recorded.** In wave 3 run `leadhigh_capqwen3-32b_goal10_audsame-H_ins0` (mini-track `hicss59-electric-energy-sy…`), a review call still failed after its three retries.
  - The frozen code ended the run as a forced exit (`review_http`), with the Doer's list after two audits and two revisions as the output. This is how it ends a run whose Auditor reply is cut off or unreadable (amendment no. 5).
  - Section 11 would call this run failed and rerun it once. Because the frozen code did not mark it failed, the rerun did not take it, and a rerun now would mean replacing a collected row by hand.
  - The run is kept as recorded and is listed, with its exit reason, beside the failure table.
  - It is the only such run in either arm. The API-hosted arm, which carries every confirmatory test, has none.

*Hand checks (amendment no. 5).*
- **Sheets and instructions.** The six coding sheets of the tag-2 note and the coder instructions (SHA-256 `ea4b1a18804d00699a9d490ed4d25badc158f8efb2d7d9057414bba8bd137a82`) went to PC and Rain at 19:31 on 8 November, after the `prereg-tag2` release. The instructions give the questions and answer letters, and they do not say what the rule predicts.
- **The coding page.** The coders worked on a coding page that holds only the sheet columns. It was published five times:
  1. 19:57 on 8 November: the instructions' questions and answers, with saving and export;
  2. 22:38 on 8 November: a note box with four note tags;
  3. 18:57 on 9 November: a way to remove an answer;
  4. 03:05 on 10 November: a coding manual with a rule and examples for each sheet, and a request to re-check earlier answers;
  5. 03:19 on 10 November: a one-sentence key rule for each sheet.

  The text of each version, with SHA-256 sums, is kept for the replication package. 59 of PC's answers and 3 of Rain's were last changed before version 4. The page does not record whether those cases were re-read.
- **Two rule questions.** Two coder-rule questions were left at their stated defaults: a U with a note stays U, and a preprint record is judged as shown.
  - Counting all five U answers as agreement would give 18 and 74, still under both bars.
  - Two venue cases whose record is a preprint server (venue-096, venue-058) were coded Y from where the paper appeared, not from the record as shown. They are scored as given. The venue check sets no rule.
- **Who coded what.** Each case was coded by one coder, half by each, as the draw assigned them. No case was coded by both, so these checks report no inter-rater statistic. Three answers PC entered under Rain's case IDs were stored under PC's own account. They are on neither sheet and were not scored.
- **Filed sheets.** PC's last save was at 19:22 on 11 November and Rain's at 01:35 on 12 November. The filled sheets were filed at 01:41 on 12 November. Each one differs from its handed-out sheet only in the answer and note columns.

| Filled sheet | SHA-256 |
| --- | --- |
| Near miss, PC | `5c9951b475894ec876e976c4d5f6767993e128fb945d4871e524dd995753307e` |
| Near miss, Rain | `ed69d42dfe2d3c8ef74097786ba413676f2d3402d308def2a7afb55c78be66bb` |
| `title_only`, PC | `3cb6b2a672e6d67f64dfe0ed999fa9ff550d3112f79816f346cc949d548b39f9` |
| `title_only`, Rain | `be1adec66a2a45db731acabbafdcd2bf46141dbebebc749bb532574238532af2` |
| Venue, PC | `c0ed9295ba772f666bb63ab6b71c6185b93b5d47049a7dc799a629ea237d774d` |
| Venue, Rain | `3ecf8cbc9d5413187e891a95d11d80d374459543924e8b78d8fe36530cf0aee2` |

*Scores.* `score_handchecks.py` (SHA-256 `ba7ce8fae17088814d4093288df2ddb6ed130c8d319f054a7085d4e47471162e`) scored the sheets at 01:43 on 12 November against the key (`b951672952e29d08f7c085b4e0d0994cb5bcef1c136a0cc1f471c1b4152d38b6`), with no sheet problem. In the near-miss and `title_only` checks a U is not agreement with the rule. Its output is [registration/handcheck\_scores.md](registration/handcheck_scores.md), with a machine-readable copy [registration/handcheck\_scores.json](registration/handcheck_scores.json).

| Check | Answers (PC; Rain) | Score | Bar | Decision |
| --- | --- | --- | --- | --- |
| Near miss, cited author on the record (rule: same work) | S 9, N 15, U 1; S 7, N 17, U 1 | 16 of 50 | 45 of 50 | Not used: its citations stay `unresolved` |
| Near miss, no cited author on the record (rule: not the same work) | N 25; N 25 | 50 of 50 | 45 of 50 | Used: its citations are `fabricated` |
| `title_only` (same work, wrong authors) | S 33, N 16, U 1; S 38, N 10, U 2 | 71 of 100 | 90 of 100 | The author rule does not join: `title_only` stays `unresolved` |
| Venue (agreement with the verifier) | Y 25, N 25; Y 26, N 24 | 68 of 100 | none; under 90, the venue matching is reviewed | Reported only |

*Decisions file.* Code commit cc939c70f1706bfbf7be317a57bc49e448cd97ec (on 6069c884; no hashed file changes, and `study_b1/HASHES.sha256` is still `8bcce5ca11b32a622dbe18b010e35f8fd08eeea70141f353dbc7806b8d15e474`) fills `study_b1/dv/handcheck_decisions.yaml` with 16, 50, 71 and 68 (SHA-256 `1a5529044670679946a9b0438e0b7cc062d97f7c39485dcaff3e1897a23bf7b5`). [registration/handcheck\_decisions\_tag2b.yaml](registration/handcheck_decisions_tag2b.yaml) is a copy. It differs from the frozen null file (`d9d121a6e0e17ae15a4fae34fff591c451f29d50a15fc1cc5301b53f6596aed7`) only in those four values. The frozen code reads it as: near-miss branch with a cited author off, branch without one on, and the author rule off. This selects the registered row `author=not_used, noauthor=used, title_only=does_not_join` of [registration/tag2\_values.md](registration/tag2_values.md):

| Doer | Ceiling |
| --- | --- |
| Claude Haiku 5.5 | 0.300 |
| Claude Sonnet 5.5 | 0.025 |
| DeepSeek Flash | 0.201 |
| DeepSeek V4-Pro | 0.146 |

The tolerances are those of the same row. In pilot stage 3 this row leaves 6.4% of API-hosted citations unresolved, from 0% to 13.6% by cell. Before the file was filled, the full test suite passed as at tag 2 (324 passed, 2 skipped). After the code commit it gives 322 passed, 2 skipped and 2 failed. The two failures are the tests that assume the tag-2 null file (`test_decisions_follow_the_registered_bars` and `test_rules_refuse_pending_decisions_but_take_a_full_what_if`). They fail as designed, and neither is edited.

*Venue check.* `venue_agree` uses the definition frozen in the null file: answers matching the verifier, out of 100. A match is Y on a case the verifier judged the same journal, N on one it judged a different journal, and U on one whose journal name it marked uncertain. No coder used U, so the score equals the agreement on the 80 decided cases: 68 of 80, or 85% (Wilson 95% interval 76% to 91%). Being under 90, the venue matching was reviewed case by case.
- **Same journal, coded N (4 of 40).**
  - One is a coder slip: "Human Factors", whose record carries its subtitle. It is described, not corrected.
  - The verifier also marked the other three uncertain, and they keep its label (amendment no. 5).
  - Without those three, the matches by ISSN-L or alternate name agree in 33 of 34 cases (85% to 99.5%).
  - All 13 cases the verifier labelled compliant were coded Y, so no matching error reaches `compliant_count`.
- **Different journal, coded Y (8 of 40).**
  - Six are real proceedings papers cited under a short form of their real proceedings name: CHI, CSCW, FAT* twice, EMNLP and NAACL-HLT. The DV specification counts such a citation as `off_venue`. The verifier labels it `misplaced`, because it does not expand conference acronyms. That is 6 of 40 sampled `misplaced` labels, or 15% (7% to 29%).
  - The other two are the preprint records above. The specification lets the published record decide, and the verifier follows it.
- **What the gap moves.** It moves citations between two non-compliant labels only. `misplacement_rate` (one of H9's four DVs) is overstated, and the exploratory `venue_violation_rate` is understated. `compliant_count`, `fabrication_rate`, `year_mismatch_rate`, `rehomed_rate` and the ceilings do not depend on it.
- **No fix.** The verifier and every labelling rule stay as frozen. The registered `misplacement_rate` tolerance was computed with this verifier, and a change made because of this check would be post hoc. No reclassification analysis is added. The paper reports, beside H9's `misplacement_rate` result:

  > The verifier does not expand conference acronyms, so a real proceedings paper cited under a short form of its proceedings name (for example "CHI" or "EMNLP") is labelled misplaced, while the DV specification counts it as off-venue. In the pre-registered venue hand check on pilot data, 6 of 40 sampled misplaced labels (15%; Wilson 95% interval 7% to 29%) were such papers. misplacement_rate is therefore overstated and venue_violation_rate understated, and the H9 contrast on misplacement_rate is affected only as far as Auditor tiers differ in how many such papers stay in final lists. compliant_count, fabrication_rate, year_mismatch_rate and rehomed_rate do not depend on this distinction.

*After this tag.*
- **Labelling.** Labelling follows amendment no. 5 and the tag-2 note:
  - the Crossref and local-copy label pass;
  - the 10% draw by `sample_openalex_main.py` (SHA-256 `382cdab2736862adff17adf3e8261ea0e713adb9af580cf8688594e8743eaa74`);
  - the live searches within the cap of 23,000 searches, or $23;
  - the final cache-only pass;
  - the labelling rules with the decisions above.

  The OpenAlex top-up approved on 8 November comes before any paid search. A new key with a prepaid balance has been in use since 12 November.
- **Main-run near-miss check.** After the label pass, a person checks citations decided by the near-miss rule, and the agreement is reported. This changes no label. Only the branch without a cited author decides citations, so the check is that branch's 50. They are drawn with seed 20261107 from the main-run API-hosted citations the branch decided, by a draw script named by its SHA-256 in a dated note before the draw. They are coded blind on the same sheet design as the pilot check.
- **Verifier validation.** The registered validation of the verifier, 100 citations double-coded blind by two coders, has not run. It changes no rule and is done before the verifier's results are reported.

When this note was written, these data existed:
- the main-run drafts and reviewed runs of both arms;
- the Crossref cache above;
- the hand-check sheets, filled sheets and scores.

No main-run label or DV existed.

**Note on the main-run final label pass (2026-11-11, US Eastern).** Times are UTC, on 12 November. The live searches of
amendment no. 5 ran as registered. The cap was 23,000 searches, and 16,187 were billed. The 3% trigger fired for every
Doer's revision list and for no draft list.

The chain's final check was fixed before labelling began, and it stopped the chain at 04:26. It had found 2,596
citations whose final-pass label used an OpenAlex answer, although the registered route gives them no live search. The
cause is in the frozen verifier. It keys its OpenAlex cache by title, and whenever OpenAlex is among its sources, it
reads any cached answer for a citation's title, whatever the citation's route. So in the cache-only final pass, a
citation outside the searched sets read the answer of a searched citation with the same title. By kind of miss, the
2,596 were:
- 1,387 approved-journal misses;
- 1,089 off-list misses outside the triggered lists;
- 120 others.

Had those answers been kept, 222 of the 2,596 would have counted as real works instead of fabricated or unresolved.

The labels used for the DVs follow amendments no. 2 and 5 as written. Each citation's label row is one of two unedited
outputs of the frozen verifier, chosen by registered set:
- the 762 poorly indexed misses and the 9,832 citations of the triggered lists take their final-pass label;
- every other citation takes its label from the first pass, made with Crossref and the local copy before any OpenAlex
  answer existed (sha256 `4e7d6681cdafab79d2c4190e698b42df9e87b8f9bb8e55f2ee342684b5664ca3`).

The merge script is `merge_final_labels.py`, SHA-256 `ba736b6a1655864b5414ab291058d0b89ceafda08121329b6a4d8c979404e78e`.
It computes no label. It stops, writing nothing, unless every row outside the two sets that changed between the passes
is one of the 2,596. On the merged labels, the final check finds no stray answer. The merged labels used for the DVs
have sha256 `51d01385634374583bf598935de9e8d3cbcf93f3e198eeab74f31ca9fe73545a`. The script, its report and the 2,596
citations, with the labels they would have had, are published with the replication package.

**The two source errors.** In the final pass, two triggered citations had a source error instead of an answer. Each was
searched once more, as section 11 does for a failed item:
- the V4-Pro revision citation got an answer and its label;
- the Flash revision citation got a source error again. It keeps the label the frozen rules give an off-list miss with
  no answer, and it is listed as a technical failure.

**One tier difference.** Comparing the merged labels before and after that retry showed one further difference. One
poorly indexed citation's record carries the ISSNs of two approved journals of different tiers. The frozen verifier
gave it tier A\* in one pass and A in the other, because it takes the first approved ISSN from a set whose order
depends on the Python process. The citation is outside the year window in both passes. The tier enters only the
descriptive A\* share of compliant citations, so no DV changes, and the labels are used as written.

No registered rule, bar or hashed file changes. The merge rule was set at 04:31 and the script's hash was named at
04:35. The script was read and confirmed at 04:38, and the merge ran at 04:38. This note was pushed afterwards,
before any rule, DV or analysis output existed.

**Note on the verifier validation (2026-11-12, US Eastern).** Times are UTC. Section 10 registers a validation of
the verifier: 100 citations coded blind by two coders, changing no rule. This note fixes how the 100 are drawn, coded
and reported, before the draw.

*The draw.*
- **The frame** is the unique API-hosted main-run citations whose final label, after the registered rules, is real
  (11,287) or fabricated (85,130). The labels file is `rules_api/labels.jsonl` of the main-run analysis, sha256
  `b7190f51d0bb131a31d3394b56e6fc892c26f454bfa020a5c300250ccfaa1c59`. The 7,029 citations left unresolved are not in
  it, because no rate uses them. Every citation in the frame has a title.
- **The cells.** Fifty are drawn with `existence` fabricated and fifty with `existence` real. Each Doer has 25 cases:
  13, 13, 12 and 12 fabricated and 12, 12, 13 and 13 real, for Haiku, Sonnet, Flash and V4-Pro in that order.
  - A citation is eligible for every Doer that cited it, and it can be drawn once.
  - There is no quota by labelling route. The key records each case's route.
- **The procedure.** One `random.Random(20261107)` draws the eight cells in that order: fabricated first, then real.
  In each cell it draws from the sorted keys not yet drawn. Then it shuffles the 100 once for sheet order.
- **The script** is `draw_verifier_validation.py`, SHA-256
  `8683f76bec6c31211a5f68e5fcdea29ae0ac0f7bdc1f3dd87146e0fd3c0481b0`. It runs on the frozen code (`cc939c70`) and
  makes no request.

*The coding.*
- The sheet shows each citation's title, authors, year and journal as the Doer wrote them. No Doer gave a DOI. It
  shows no database record and no verifier label.
- Both coders code all 100, blind to each other and to the key. They look each citation up themselves and do not use
  the study's run files.
- The question is the test of the pilot hand checks: "Would a librarian hand you this exact paper from what the Doer
  wrote?" The answers are:
  - **S**: a real published work this citation identifies, even with wrong authors, year or journal;
  - **N**: it does not exist, or only a different paper shares some of its words;
  - **U**: cannot settle.

*The report.*
- Raw agreement and Cohen's kappa, with 95% intervals.
- For each stratum, the verifier's precision, counted over the cases where both coders gave the same S or N, with a
  Wilson 95% interval: for verifier-fabricated, the share agreed N; for verifier-real, the share agreed S.
- Overall accuracy, weighting the two strata by their sizes in the frame.
- Precision by labelling route, as a description.
- Cases with a U or a disagreement are counted and listed, not adjudicated.

The validation changes no rule and no label.

*When this was fixed.* When this note was written, the main-run labels and the main-run analysis existed. The draw
script had been written and hashed at 12:44, and no validation case had been drawn.
