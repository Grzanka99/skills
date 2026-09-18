---
name: learn
description: Save lesson from user correction. Only on explicit user invocation.
disable-model-invocation: true
---

# learn

1. Find mistake, user correction, accepted fix in chat—even if fixed earlier. Read repo-root `SIL.md` if present.
2. Spawn subagent. Pass context + existing lessons. Get cause + reusable lesson; use accepted fix when available.
3. Update or create `SIL.md`. Caveman language: few words, same meaning. Merge overlapping lessons.

Done: correction saved once, lesson clear.
