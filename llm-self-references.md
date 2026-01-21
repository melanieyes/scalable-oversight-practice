# LLM Self-Preference Paper Replication (Notebook)
This notebook is a lightweight replication of a common “**self-recognition / self-preference**” evaluation setup for LLM-generated summaries.

It tests whether a judge model can:
1) **Recognize** which summary was written by a target model (“self-recognition”), and  
2) **Prefer** the target model’s summary over an alternative (“self-preference”).

## What the notebook does
- Loads summarization datasets (e.g., **XSUM** and **CNN/DailyMail**).
- For each article, generates:
  - `S_self`: a summary from a chosen “self” model (default: `gpt-4.1-nano`)
  - `S_other`: either **human reference** summaries *or* another model’s summaries (e.g., `gpt-4o-mini`)
- Builds paired examples (`self vs other`) and runs a **model-vs-model** and/or **model-vs-human** evaluation.
- Uses **swap-and-average** (presenting summaries in both orders) to reduce **position bias**, then estimates the probability the judge picks the SELF summary.

## Key metrics
- **Mean self-recognition**: how often the judge correctly identifies the self model’s output.
- **Mean self-preference**: how often the judge *chooses* the self model’s summary as better.

## Setup
### Dependencies
The notebook installs the required packages (e.g., `openai`, `datasets`, `tqdm`, `python-dotenv`).

### API Key
You need an OpenAI API key available to the runtime (environment variable or Colab `userdata`).

## How to run
1. Open the notebook in Colab / Jupyter.
2. Run cells top-to-bottom.
3. Start with a small `N` (e.g., 50) to sanity check, then scale up (e.g., 1000).

## Useful knobs to edit
- `N`: number of evaluation pairs (controls runtime + cost).
- `MODEL_SELF`: the model whose “self” behavior you’re probing.
- `MODEL_OTHER`: the alternative model (if doing model-vs-model).
- `USE_HUMAN_OTHER`: switch between **vs Human** and **vs Model** conditions.

## Output
At the end, the notebook prints a compact summary table of:
- dataset × condition (vs human / vs model)
- `mean_self_recognition`
- `mean_self_preference`

## Why this matters (AI safety / evals angle)
This is a simple stress test for **model identity cues** and **preference bias**. If a model reliably recognizes its own outputs or systematically prefers them, that can affect:
- evaluations that rely on LLM judges,
- ensemble systems,
- and any pipeline where “who wrote this?” or “which is better?” matters.
