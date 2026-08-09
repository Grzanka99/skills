---
name: orchestrate
description: Orchestrate a big task or plan into subagent waves — split into chunks, spawn implementation subagents, integrate results. Use when the user asks to orchestrate or parallelize work across subagents, or hands you a plan too big for one context.
---

# Orchestrate

You are the **orchestrator**. You hold the whole plan; each subagent implements one **chunk**. You decompose, sequence, delegate, and integrate — you never implement a chunk yourself, only small glue fixes between waves. Track chunks and wave state in your todo list.

## Steps

1. **Decompose** the goal into chunks one subagent can finish autonomously. Read any referenced plan file first — never decompose from a path alone. Scout the codebase first if file ownership is unclear. Split so parallel chunks never write the same file — two chunks that need the same file become one chunk, or land in different waves. If a chunk needs the whole plan explained, split it further; if it is a one-line change, fold it into a neighbour. Complete when each chunk has a goal, owned files, and a checkable completion criterion (named tests or a command that must exit 0).

2. **Wave** the chunks: each chunk gets the earliest wave after everything it depends on. Independent chunks share a wave and run in parallel. Default to one subagent at a time; parallelize only when chunks are truly independent — wider waves multiply integration work. Cap a wave at 2–5 chunks. Complete when no chunk shares a wave with a chunk it depends on.

3. **Spawn** the wave: one subagent per chunk, all launched in a single message so they run in parallel. Use the implementation subagent your environment provides (e.g. `workhorse`, `general`). Subagents start with zero context — every prompt follows the contract below. Complete when every chunk in the wave is running.

4. **Integrate** the wave: read every report, then verify yourself — run each chunk's completion checks rather than trusting claimed results; intermediate waves may stay incomplete by design, so save the full build and test run for after the final wave. Fix integration glue inline; send chunk-owned failures back to their owner or respawn them as a new chunk carrying the failure details. Start the next wave only when this one verifies clean. Complete when the final wave verifies clean and the whole goal's checks pass.

5. **Review** the combined diff with one read-only review subagent. Send each material finding back to its chunk's owner; dismiss the rest and record each dismissal with a one-line reason. A dismissed finding is settled while the code it concerns stays unchanged — later rounds never resurrect it, and you never spawn fixes for it; if a fix touches that code, the finding is fair game again. You may stop after two fix-and-review rounds unless new findings are material and not repetitions of settled ones; when you stop, report leftovers as risks instead of fixing them. Complete when no material findings remain or you stop the loop.

6. **Finish**: report changes, checks, review outcome, and risks. Leave all changes uncommitted unless the user asks.

## Prompt contract

A subagent sees nothing but its prompt. Each spawn includes:

- The chunk's goal and boundaries: what to change, what to leave alone.
- Exact file paths, plus the conventions and patterns to follow.
- The completion criterion and how to verify it.
- The report format: files changed, verification output, deviations or blockers.
