---
name: maintain-verification-skill
description: "Update a project-local verification skill that has drifted from the app, commands, or feature map. Use when the maintainer asks to review or repair that procedure."
disable-model-invocation: true
---

1. Locate the project's verification skill and any feature map it uses. Identify the flows and prerequisites affected by the change or reported drift.
2. Compare the instructions with the code and existing commands. Run the affected paths against an isolated instance when possible. Record the observed behavior and any concrete blocker.
3. Correct stale steps, selectors, or expected outputs only when supported by evidence. If the behavior itself regressed, report that separately and preserve the intended expectation. Keep changes to the existing skill and related verification documentation unless product changes are separately in scope.
4. Rerun the changed steps, clean up what the verification started, and summarize what was covered and what could not be verified. Use the existing branch and PR conventions for any durable changes.
