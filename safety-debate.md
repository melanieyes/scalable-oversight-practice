# AI Safety via Debate — Mini Simulation

This is a small “AI Safety via Debate” toy project that demonstrates how **persuasion can conflict with truth** when a judge only sees arguments, not the underlying evidence.

## What it does
- Spins up **two debaters**:
  - **Alice (Honest)**: argues for the objectively correct answer using the hidden text.
  - **Bob (Liar)**: is forced to argue for a **specified incorrect answer** (persuasive misinterpretation).
- The **Human Judge (you)** only sees the debate transcript.
- After you pick a winner, the script **reveals the hidden text** so you can check whether you were fooled.

## Why this matters (AI safety angle)
This mirrors a key safety concern: models can produce **confident, persuasive outputs** that sound right even when they’re wrong. Debate is a way to:
- pressure-test claims,
- surface missing assumptions,
- and reward arguments grounded in **quotable evidence**.

## How to run
1. Install dependencies (example):
   - `openai`
   - `anthropic`
   - `termcolor`
2. Set your API keys:
   - `OPENAI_API_KEY`
   - `ANTHROPIC_API_KEY`
3. Run the notebook/cell to start the debate UI.

## Controls (Judge input)
At the end of each round:
- Press **Enter** → continue
- Type **alice** → choose Alice as winner + reveal hidden text
- Type **bob** → choose Bob as winner + reveal hidden text
- Type **q** → quit

## Notes on implementation
- Uses **Anthropic (Claude Haiku)** and **OpenAI (GPT-4o)** with a fallback: if Anthropic fails, that debater switches to OpenAI.
- Adds input validation so only valid judge actions are accepted.
