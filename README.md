# 100 Kaggle first-place solutions

Data behind the write-up on what wins Kaggle competitions. It covers the last 100 competitions with a published first-place writeup, with deadlines from November 2023 to September 2026.

## Files

`solutions.csv` has one row per winning solution. It lists the competition, its type (Featured, Research or Playground) and domain (structured, unstructured, llm or other), the final models and methods, and a link to the writeup. `source_access` shows whether the full writeup was readable, only part of it, a mirrored copy, or nothing.

`techniques.csv` has one row for each technique mentioned in a writeup, 1,161 rows in total from the 98 readable writeups. Each row says what the winners did, why it helped and when it applies, and includes a short quote from the writeup. `canonical` links rows that describe the same recurring trick. `mainstream` is a rough guess at whether an average data scientist would already know the technique.

`usage.json` counts how many solutions in each domain used each model and method. These counts are the source of the percentages in the write-up: XGBoost appears in 18 of 40 structured solutions, for example, which is 45%. `tagged` is the count from the first pass alone (see below), and `na` lists the domains where a method doesn't apply.

## How it was made

The competition list comes from [Meta Kaggle](https://www.kaggle.com/datasets/kaggle/meta-kaggle). Writeups were found through [faridrashidi/kaggle-solutions](https://github.com/faridrashidi/kaggle-solutions), with a [Hugging Face mirror](https://huggingface.co/datasets/t2ance/mle-skills-kaggle-writeups-clean) for a few that wouldn't load. Community and judged-only competitions are left out. The final set has 40 structured, 31 unstructured, 17 LLM and 12 optimization or simulation competitions.

The data comes from two passes with LLM agents:

1. GPT-6 Luna agents (low effort) tagged each solution's domain, models and methods. Their output was then checked by hand. The main fixes were wrong links and models that were tried but didn't make it into the final submission.
2. Claude Sonnet 5.5 agents (medium effort) read every writeup in full and wrote down each technique with a supporting quote. A script checked that every quote appears in the writeup, and repeated techniques were grouped by hand.

A method counts in `usage.json` if either pass found it.

## Limitations

Winners don't write down everything they did, so read the numbers as minimums. A missing tag means the writeup didn't mention it, not that it wasn't used. Two writeups couldn't be read at all, and a few solutions don't say which model they ended up with (`unknownModels` in `usage.json`).
