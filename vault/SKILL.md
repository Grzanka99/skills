---
name: vault
description: Second-brain management for the user's Obsidian vault. Use when the user asks to remember, save, recall, or search personal information; requests note management; or mentions their vault, Obsidian vault, or second brain.
---

# Vault

Treat `/Users/cezary/Desktop/Vault` as a living second brain whose structure is agent-managed.

1. Choose the executor. Prefer a subagent with low reasoning effort for vault operations. Work directly when that is clearly simpler or more reliable. When delegating, pass the request, vault path, working-set boundaries, and permitted operations. Complete when the executor has a precisely bounded task.

2. Establish the working set:
   - `Archived/` is a hard boundary: omit it from reading, searching, indexing, writing, moving, and deletion.
   - Omit `Job/` and `What To Code/` by default. Include either only when the request names it or unmistakably concerns job notes or coding ideas.

   Complete when every candidate path is inside the working set.

3. Perform the requested branch:
   - **Capture:** Search related notes first. Integrate the information where it fits, or create and organize a suitable note.
   - **Recall:** Search the working set, synthesize the relevant knowledge, and identify the source notes.
   - **Manage:** Create, edit, rename, move, consolidate, or delete notes and folders as useful. Before deletion, verify that the content is obsolete, redundant, or safely consolidated. Preserve it and ask when unique information may be lost.

   Complete when the knowledge is retrievable, the request is satisfied, and every affected path respects the working set.

4. Briefly report the result and material changes, including affected note paths. Complete when the user can tell what was found or changed.
