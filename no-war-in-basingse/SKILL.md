---
name: no-war-in-basingse
description: Use ONLY when the user says "no forest", "basingse rule", "no war in basingse", or explicitly asks for a basingse/no-forest check. Finds rules that mention things which cannot happen in the target.
---

# no-war-in-basingse

Audit the target the user points at.

Use this on instructions, comments, docs, tests, or code.

## The test

Check each relevant line:

1. **Can this happen here?**
   Check schema, types, code, product shape, and surrounding context.
2. **If it cannot happen, remove the line.**
   No rewrite. No softened version. No explanation in the target.
3. **If it can happen but is written as a ban, prefer the positive behavior.**
   Keep the ban only when the positive version loses safety or clarity.

## Example

Schema has no `status` field:

> Do not output task status.

Delete it. `status` is dead.

Real risk:

> Never commit secrets to the repo.

Prefer: `Store secrets in the vault; keep them out of commits.`

Keep the ban if that is clearer.

## Completion

Classify every relevant line as clean, impossible, rewritten, or kept as a hard guardrail.
