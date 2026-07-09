---
name: planning
description: Plans: use when creating or maintaining documents in plans/<plan-name>/.
---

# Planning Skill

## Structure

Each plan lives in:

```text
plans/<plan-name>/<plan-files>
```

Its source of truth is:

```text
plans/<plan-name>/index.html
```

Supporting artifacts use:

```text
XY_descriptive_name.html
```

`XY` is a two-digit ordering prefix. Plan documents are self-contained HTML with inline CSS and no dependencies. Inline JavaScript may improve usability, but content remains complete without it.

The `plans/` directory may be an independent Git repository. Treat its Git history, status, and commands independently from any parent repository.

## Workflow

1. Work within the selected `plans/<plan-name>/` directory. For an existing plan, read `index.html` first, then its linked artifacts or files the user names. For a new plan, create its directory and `index.html`. Complete when its goal, status, next action, and relevant context are understood.
2. Create or update `index.html` with the required content below. Add `XY_descriptive_name.html` only when it clarifies the plan, and link every artifact from the index. Complete when the index represents the current plan state.
3. When the plan state changes, record completed actions, status, and the following concrete action in `index.html`. Complete when the index remains current.

## Required `index.html` Content

Present these sections in a clear, usable layout:

- Plan name and goal
- Status: `draft`, `active`, `blocked`, or `done`
- Next Action: the next concrete thing to do; after completing it, update progress and decide the following action
- Progress: completed actions, current phase, and important status updates
- Files: links to each `XY_descriptive_name.html` supporting artifact
- Notes: important context, decisions, or links
