---
name: correct
description: "Use when asked to stop a recurring project mistake. Find evidence from prior changes, choose a durable way to catch or prevent it, and prove the correction."
disable-model-invocation: true
---

1. Find instances of the same mistake in corrections, reviews, reverts, tests, or repository history. Look for at least two instances and confirm the common cause before treating it as recurring.
2. Prefer a simple code structure that makes the correct path clear. Consider types, an existing lint or CI check, or a focused behavioral test when they can enforce the constraint with proportionate effort.
3. Use prose for judgment or project conventions that code cannot reasonably enforce. Add durable, verified guidance only to the repository-specific section of `AGENTS.md`, an appropriately scoped instructions file, or the existing project documentation. Follow the maintainer's authorization rules for changes to shared instructions or skills.
4. Prove the correction on the original failure when practical and confirm valid behavior still works. Use the project's existing validation setup. In the PR or hand-off, cite the recurring examples, the enforcement point, and what was verified.
