# Amendments

Changes to [PREREGISTRATION.md](PREREGISTRATION.md) or to any frozen file made after the `prereg-tag1` tag. Each entry gives:
- the date;
- the section changed;
- what changed and why;
- which study data, if any, existed at that time.

| No. | Date | Section | Change | Reason | Data existing at the time |
| --- | --- | --- | --- | --- | --- |
| 1 | 2026-11-06 (US Eastern) | 11 (Exclusion and stopping rules), 7 (pilot additions); DV specification section 7 | The cut-off rule now applies only to a reply that stops at the output limit and cannot be read. A reply that stops at the limit but holds a complete, readable JSON object is used like any other reply; the text after the object is stored, not scored. Such replies are counted and reported by cell and role as a new data-quality share. No code or hashed file changes. | Pilot stage 1 showed that the registered text and the frozen code differed: the code, as hashed at `prereg-tag1`, already treats a readable reply this way, which matches Appendix B (text outside the JSON object is stored, not scored). The text is brought in line with the code instead of changing the code, so no valid list is thrown away. | Pilot stage 1 only (1 pilot mini-track). Pilot data never enter the analysis. No main-run data existed. |
