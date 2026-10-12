# 100 Kaggle first-place solutions

A dataset of the models, methods and techniques used in the 100 most recent Kaggle competitions with a published first-place writeup.

## Files

- **`solutions.csv`**: one row per winning solution (100 rows).
  `sample_number`, `title`, `slug`, `deadline`, `publication_date` (of the writeup), `kind` (Featured / Research / Playground), `domain` (structured / unstructured / llm / other), `subdomain`, `models`, `methods`, `tuning`, `source_access` (full / partial / mirrored / unavailable), `source_url`, `pipeline` (short summary), `notes`.
- **`techniques.csv`**: one row per technique per writeup (1,161 rows from 98 readable writeups).
  `slug`, `i` (row index within the writeup), `canonical` (id of the recurring technique the row was grouped under, if any), `trick`, `stage`, `mainstream` (yes / partly / no), `worked`, `gain` (as reported), `what`, `why`, `when`, `quote` (verbatim from the writeup).
- **`usage.json`**: counts of solutions per domain using each model family, model and method. Shares in the accompanying essay are these counts divided by `n`.

## Methodology

**Sample.** The latest 100 Kaggle competitions with a published first-place writeup, with deadlines from 2023-11-30 to 2026-09-29 (cutoff 2026-10-05). Featured, Research and Playground competitions with finalized leaderboards are included. Community, classroom and judged-only events are excluded. Domains: 40 structured, 31 unstructured, 17 LLM, 12 other (optimization and simulation).

**Sources.** Competition metadata comes from [Meta Kaggle](https://www.kaggle.com/datasets/kaggle/meta-kaggle). Writeups were found through [faridrashidi/kaggle-solutions](https://github.com/faridrashidi/kaggle-solutions), with [a Hugging Face mirror of writeups](https://huggingface.co/datasets/t2ance/mle-skills-kaggle-writeups-clean) as a fallback. Each row links to its primary source.

**Coding.** There were two passes:
1. *Solution audit* (`solutions.csv`): GPT-6 Luna agents (low effort) tagged the domain, final models and methods of each solution. I reviewed the output by hand and corrected rank and source mismatches, as well as models that had been tried but were not part of the final solution.
2. *Technique extraction* (`techniques.csv`): Claude Sonnet 5.5 agents (medium effort) read each full writeup and recorded every concrete technique, each with a verbatim quote. A script checked every quote against the source text. I grouped recurring techniques by hand.

`usage.json` combines both passes. A method counts if the audit tagged it or an extracted technique that worked describes it.

**Caveats.**
- The counts reflect what authors reported. A missing tag means "not reported", not "not used", so all shares are lower bounds.
- Two writeups could not be read, and eight predictive solutions have no verified final model.
- `mainstream` is the extraction model's judgment of whether a typical data scientist would know the technique. It is not a survey of practitioners.
