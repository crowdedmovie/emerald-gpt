---
name: create-verification-skill
description: "Turn a concrete, repeatable way of verifying a project's app, CLI, or service into a project-local skill. Use when the maintainer requests a skill for an actual verification need."
disable-model-invocation: true
---

1. Identify the real verification task and its prior run or existing procedure. Inspect the repository's documented commands, tests or tools, and expected user-visible result. If evidence is missing, perform the smallest safe verification on the intended interface before writing instructions.
2. Use the repository's existing skill convention or the skill path supported by the target runtime. Write a concise `verify-<app>/SKILL.md` with its name, trigger, and exact commands. Describe setup, readiness, test data, action, expected observable result, and cleanup. Reuse working scripts and keep evidence separate from disposable state.
3. If the project has a feature map, reference the relevant entries and add precise verification notes there when useful. Keep shared project decisions in their existing documentation.
4. Follow the recorded procedure from a clean test state for at least one representative path. Fix mismatches and confirm evidence remains accessible after cleanup. Report which path ran and any missing prerequisites. Label procedures that could not be exercised as unverified.
