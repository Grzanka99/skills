---
name: no-war-in-basingse
description: Use ONLY when the user says "no forest", "basingse rule", "no war in basingse", or explicitly asks for a basingse/no-forest check. Finds rules for impossible behavior.
---

# no-war-in-basingse

Audit user-selected instructions, comments, documents, tests, or code.

## Procedure

For each relevant line:

1. **Can this happen in the current intended product?**
   Check schema, types, code, and product structure.
2. **If no, delete the line.**
   Do not rewrite or explain it.
   If a test names an absent concept, delete the test. Do not test absence.
3. **If yes, state the wanted behavior.**
   Use a ban only when safer or clearer.

## Tests

- Test current product behavior, not history.
- Remove tests, fixtures, mocks, assertions, and bug reproductions for removed concepts.
- Keep negative tests only for invalid input still possible at a current product boundary.

Forest removed: test current land use. Do not test missing forest or trees.

## Example

No `status` field:

> Do not output task status.

Delete the instruction.

Possible risk:

> Never commit secrets to the repo.

Rewrite: `Store secrets in the vault. Keep secrets out of commits.`

## Completion

Classify each relevant line: valid, impossible, rewritten, or safety ban.
