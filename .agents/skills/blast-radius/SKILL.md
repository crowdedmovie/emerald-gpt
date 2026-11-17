---
name: blast-radius
description: "Review the impact of a proposed or existing change beyond its diff. Use to find plausible regressions and check the assumptions that make a PR safe."
---

1. Read the diff and the changed contracts. Trace affected callers and downstream dependencies, including serialized data, configuration, supported inputs, and user flows where relevant.
2. Identify the one or two assumptions that have to hold for the change to be safe. For each material risk, describe how to reach it, who is affected, and the relevant code or dependency version.
3. Verify those assumptions on the closest available real path. Prefer a focused test or running the actual app when practical. State the observed result and any risk that could only be assessed by reading.
4. Report confirmed findings, checks that cleared significant concerns, and the smallest remaining check before merge. Follow any applicable repository rules for editing or opening a PR.

When preparing a PR, see [opening a PR](references/opening-a-pr.md).
