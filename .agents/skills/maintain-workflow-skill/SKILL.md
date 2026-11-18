---
name: maintain-workflow-skill
description: "Refine an existing project-local workflow skill using maintainer feedback and evidence from prior use. Use only when the maintainer explicitly asks to review or update that skill."
disable-model-invocation: true
---

1. **Find the skill and the evidence.** Read the target `SKILL.md` and its relevant scripts, references, and project instructions. Identify the skill from the request or ask if the target is ambiguous. Keep edits scoped to the selected project-local skill. For a baseline-managed copy, point to its source repository for an update.
2. **Review what happened.** Compare the written procedure with the user's feedback and any runs or excerpts available to you. Look for missed steps, repeated clarifications, and decisions made before the user could review them. Identify where instructions were missing, unclear, out of order, or already adequate. Treat a one-off preference as task-specific unless the user wants it reused.
3. **Revise the smallest relevant part.** Apply clear, durable feedback and fix friction supported by the available evidence. Reuse or move existing instructions when that resolves the problem. Ask the user to decide any unresolved change that would materially affect scope, inputs, outputs, or approval points.
4. **Review the diff.** Check that the revised instructions address the reported friction and preserve existing conventions and agreed review points. Check that referenced files exist and that changed commands match the repository's documentation or tooling. Report what changed, what justified it, and any open questions. Maintenance ends with this written review. Run or test the revised workflow only on explicit request.
