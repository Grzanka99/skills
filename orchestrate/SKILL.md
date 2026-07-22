---
name: orchestrate
description: Orchestrate implementation with worker and review subagents.
---

# Orchestrate

Keep the parent as the control plane. Keep it read-only for implementation files. Let workers edit.

## Steps

1. Resolve the input.
   - Accept a plan path, an inline request, or the current conversation context.
   - Read a plan file before using it.
   - Ask one focused question only when the goal, scope, or completion checks cannot be inferred.
   - Complete when the goal, scope, and completion checks are clear.
   - Split the plan into focused tasks

2. Split the work.
   - Use one worker at the time by default.
   - Run workers in parallel only when packets have independent dependencies, separate ownership, and separate checks.
   - Use the fewest workers needed.
   - Complete when every requirement has an owner and dependencies are ordered.

3. Delegate implementation.
   - Prefer a named `workhorse` agent. Otherwise spawn an implementation subagent and request low reasoning effort.
   - Give each worker a self-contained work packet: outcome, relevant context, ownership, dependencies, and observable completion checks.
   - Ask each worker to inspect, edit, run targeted checks, and report changed files, checks, blockers, and risks.
   - Report a blocker when subagent spawning is unavailable.
   - Complete when every required worker is running with a complete packet.

4. Consolidate.
   - Wait for all required workers.
   - Check their reports and the combined diff.
   - Send conflicts and integration gaps to a focused worker.
   - When several workers changed related code, assign one worker to run integration checks.
   - Complete when the combined change is coherent and check results are known.

5. Review.
   - Prefer a named `review` agent. Otherwise spawn a separate read-only reviewer and request high reasoning effort.
   - Ask for actionable findings.
   - Send each finding to the worker that owns the changed area. When ownership is unclear, send all findings to one worker.
   - Run review again after fixes.
   - Aim for two fix-and-review rounds. Continue when findings remain material or fixes substantially change the diff. Otherwise report remaining risks.
   - Complete when the review result is known and material findings are fixed or reported.

6. Finish.
   - Report changes, checks, review result, blockers, and risks.
   - Leave the combined changes uncommitted unless the user asks.
   - Complete when the user can verify the result.
