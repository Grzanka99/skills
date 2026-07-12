---
name: fleet
description: Resolve and access the user's personal remote machines. Use whenever the user refers to archplate, the Arch machine, or the Arch box, including requests that require context about or SSH access to that machine.
---

# Fleet

Treat machine names and aliases as pointers to private inventory records.

## Machines

- `archplate`: aliases `Arch machine` and `the Arch box`; read `references/archplate.md`.

## Procedure

1. Resolve the user's wording to exactly one machine above and read its reference file. Complete when the machine and its stored context are known.
2. Use the stored context directly for discussion and planning. When the requested work requires live state or remote action, connect with the record's SSH command. Complete when the user's request is fulfilled on the intended machine.

Assume SSH key authentication is already configured. Treat inventory records as manually maintained reference; change one only when the user asks to update it.

Use `references/_machine-template.md` when registering another machine. Add its canonical name, aliases, and reference pointer to this file so future mentions invoke and resolve the skill.
