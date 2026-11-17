---
name: bug-fix
description: "Investigate and fix a behavior bug by reproducing it, isolating its cause, and checking the fix on the same path. Use when asked to diagnose and fix a bug."
---

1. Identify the expected behavior, actual behavior, and smallest reproduction. Reproduce on the affected interface or entry point when possible. Record the failing output or state.
2. Narrow the cause with targeted observations. Compare plausible explanations against real evidence from the code, logs, or a focused run. Trace the regression in Git when that would answer a concrete question.
3. Apply the `tdd` method when a focused executable regression test is practical. Otherwise use the closest meaningful reproduction that can be run in this environment.
4. Fix the confirmed cause with the smallest change that preserves nearby contracts. Remove temporary diagnostics.
5. Replay the reproduction on the same path. Run the relevant nearby checks and report the observed before and after results. State any verification gap and its consequence.
