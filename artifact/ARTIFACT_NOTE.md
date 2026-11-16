# Artifact Note: Study B1

**The question.** Which team structures and model choices reduce hallucination in information retrieval from a language model, and at what cost? Information retrieval, in this study, means the user obtaining information from the model itself: the model answers from its own memory, with no search or document collection involved. The study operationalises it as literature search. A team of AI agents (a Lead, a Doer and an Auditor) with no tools lists literature for 79 conference mini-track topics, and every citation it returns is checked against the bibliographic record.

**What the artifact holds.** [`b1_level1_config.yaml`](b1_level1_config.yaml) is the Level 1 research configuration. Its sections follow the call: design logic, actors and information flows, key parameters, data provenance, analytical targets (each registered hypothesis mapped to its estimand, model, deciding variable and verdict rule), replication requirements, scope conditions and the extra fields for experiments with agents. [`b1_level2_reasoning.yaml`](b1_level2_reasoning.yaml) is the Level 2 reasoning front-end: motivations, typed positioning, a concept graph, the reasoning journey and extension directions.

**How it ties to the registration.** Every value comes from the pre-registration in this repository or from frozen code named by commit and hash. If these files and `PREREGISTRATION.md` ever differ, `PREREGISTRATION.md` wins. Three tags fixed the design before the first paid call, the pilot-set values before the main run, and the hand-check results before any main-run citation was labelled. The registered labels, dependent variables and verdicts are the confirmatory results. Amendment no. 6 adds four post-registration constructs: factual hallucination, faithful hallucination, compliant (author-checked), and task cost in tokens and US dollars. They are exploratory, carry no verdict, and sit in fields marked `post_registration`.

**What an agent can do with it.**
- *Reconstruct* the study from the models, prompts, configs, task file, journal list and seeds, each named by hash.
- *Replicate* it: a replication matches if each estimate falls inside this study's 95% interval, widened by the registered run-to-run spread.
- *Validate* the labels: two coders checked the verifier on 100 main-run citations (agreement 95 of 100, Cohen's kappa 0.902; scores note in `AMENDMENTS.md`).
- *Extend* it: the scope conditions name what would change the results, such as a search tool for any role, another journal list or window, other models, or a different audit cap.

**Data and review.** The data are archived on Zenodo; [`DATA_ARCHIVE.md`](DATA_ARCHIVE.md) gives the DOI and every file's SHA-256. Local paths, batch IDs, coder names and the e-mail addresses in the stored bibliographic answers were replaced before release, and no file holds API keys or credentials. Reviewers receive anonymous copies through the journal-approved channel.

**Licence.** Upon acceptance, all artifact files (the Level 1 research configuration, code, prompts, run logs and derived data) will be deposited in a stable public archive with a DOI under open licences: MIT for code and CC BY 4.0 for data and documentation. Third-party text included for replication (the conference mini-track titles and descriptions) is shared with its source URLs and is not covered by these licences.
