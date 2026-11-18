---
name: create-workflow-skill
description: "Create a project-local skill for a concrete, repeatable task or workflow. Use only when the maintainer explicitly asks to turn a workflow or one of its stages into a skill."
disable-model-invocation: true
---

1. **Ground the workflow.** Start from a concrete example supplied by the user, a previous run, or an existing documented procedure. Read the repository's instructions and relevant docs, scripts, and skills. Ask only about gaps that materially affect scope, required inputs, outputs, or decisions the user needs to make.
2. **Define the handoff.** Identify prerequisites, inputs that vary, ordered steps, and what a completed result looks like. For one stage of a larger workflow, identify the inputs it receives and the outputs it passes on. Keep the stage usable on its own. Where the user wants to review or approve an intermediate result, make that stopping point explicit and describe what to present before continuing.
3. **Write the skill.** Follow the repository's skill conventions. By default, create `.agents/skills/<name>/SKILL.md` with a descriptive `name`, a `description` that says when to invoke it, and `disable-model-invocation: true`. Use a new, task-specific name and keep the created skill in the project. Reuse existing commands, scripts, and references. Include only the details needed to follow the workflow from the repository and its stated inputs.
4. **Review the written procedure.** Reread the `SKILL.md` against the agreed scope and example. Check that a fresh thread could identify the inputs, follow the steps, recognize the expected output, and honor the stopping points. Check that referenced files exist and that commands agree with the repository's documentation or tooling. Flag any assumptions or prerequisites you could not confirm from inspection.
5. **Hand off the skill.** Report its path, what to give it when invoking it, and any open points. Creation ends with the written review. Run or test the created workflow only on explicit request.
