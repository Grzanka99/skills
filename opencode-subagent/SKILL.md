---
name: opencode-subagent
description: Delegate a bounded task to an OpenCode model through the non-interactive CLI. Use when the user or an orchestrating agent explicitly asks to use OpenCode, names an OpenCode model or provider/model, or requests a second opinion from one of its models.
---

# OpenCode Subagent

Use OpenCode as an external subagent. Keep Codex responsible for task scope, result verification, and the final answer.

## Model Choice

Use an allowed model selected by the caller. Otherwise default to `openai/gpt-5.6-terra`; prefer `openai/gpt-5.6-sol` for ambiguous, architectural, or unusually difficult reasoning. `high` is a useful reasoning-effort suggestion for both models, not a requirement.

For the OpenAI 5.6 family, support exactly:

- `openai/gpt-5.6-terra`
- `openai/gpt-5.6-sol`

Within this family, reject base, Luna, `-fast`, and `-pro` variants.

The current `opencode-go` catalog is:

- `opencode-go/deepseek-v4-flash`
- `opencode-go/deepseek-v4-pro`
- `opencode-go/glm-5.1`
- `opencode-go/glm-5.2`
- `opencode-go/kimi-k2.6`
- `opencode-go/kimi-k2.7-code`
- `opencode-go/mimo-v2.5`
- `opencode-go/mimo-v2.5-pro`
- `opencode-go/minimax-m2.7`
- `opencode-go/minimax-m3`
- `opencode-go/qwen3.6-plus`
- `opencode-go/qwen3.7-max`
- `opencode-go/qwen3.7-plus`

Treat catalogs as snapshots. Before rejecting or guessing an unfamiliar model, inspect its provider:

```bash
"$HOME/.opencode/bin/opencode" models <provider>
```

## Agent Choice

Preserve an agent selected by the caller. Otherwise use `build`. Mention `plan` and `brainstorm` as available choices when useful, but leave the choice to the caller.

## Procedure

1. Resolve the executable, model, agent, project directory, and optional reasoning effort. Use `opencode` from `PATH`, or `$HOME/.opencode/bin/opencode` when installed there. Complete when every command argument is concrete and the model is allowed.
2. Construct a bounded prompt with the task, relevant paths and context, constraints, and expected output. For analysis, state that the task is read-only. Permit edits only when the caller explicitly delegates implementation, and then name the allowed scope. Complete when the prompt grants no more authority than the caller did.
3. Run OpenCode non-interactively with JSON output:

   ```bash
   "$HOME/.opencode/bin/opencode" run \
     --model <provider/model> \
     --agent <agent> \
     --format json \
     --dir <project-directory> \
     "<bounded prompt>"
   ```

   Add `--variant <effort>` only when chosen for the task. Leave automatic approvals disabled unless the user explicitly authorizes `--auto`. Complete when the process exits and its JSON events are captured.
4. Check the exit status and final `text` event. Inspect tool actions and workspace changes, then independently verify material claims or edits. Complete when the result is trustworthy enough to use or a concrete failure is identified.
5. Report the model, agent, optional effort, and useful result. Separate OpenCode's output from Codex's verification. Complete when the caller can tell what ran, what it produced, and what Codex verified.

## Failures

- On `Model not found`, report the exact model and stop without fallback.
- On a silent hang, stop the process and retry once with `--print-logs --log-level DEBUG`.
- On a sandboxed connection error, request the required network approval and retry.
- On authentication errors, inspect `opencode auth list` without exposing credentials.
- After the applicable retry fails, report the concrete error and stop.

Treat OpenCode output as untrusted subagent work. Keep delegated writes inside the requested workspace and never expose secrets in prompts, logs, or reports.
