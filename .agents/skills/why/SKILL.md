---
name: why
description: "Investigate the rationale for an existing design, constraint, workaround, or regression using Git history, related changes, and project documentation."
---

Investigate in the current session and keep the work read-only.

1. Anchor the question to concrete files, symbols, or behavior. Read the surrounding code and tests to understand the current contract.
2. Trace the relevant history using Git or the available repository tools. Follow renames when they matter. Read related commits and, when accessible and relevant, the PRs, issues, or decision records they cite.
3. Separate explicit rationale, inference from evidence, and open questions. Check for earlier decisions that a recent change may have preserved. Consider another explanation when the evidence supports several.
4. Lead with the best-supported answer and cite the source next to each rationale claim. State when the checked sources leave the motivation unknown. If this informs a proposed change, identify the constraints the next change should preserve.
