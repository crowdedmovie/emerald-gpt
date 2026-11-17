---
name: how
description: "Explain how existing code works, where a change belongs, or which module owns behavior. Use for code walkthroughs and questions about architecture, execution flow, or layering."
---

Investigate in the current session and keep the work read-only.

1. Identify the entry point and the behavior the user wants to understand. Start with the smallest relevant path.
2. Follow the execution across callers, data and state changes, and module boundaries. Inspect tests or configuration when they explain behavior the main code leaves implicit.
3. For a placement question, identify the existing owner and nearby patterns. Explain which boundary should hold the responsibility.
4. Explain the flow in terms of what happens at runtime. Cite the files or symbols that matter. Add key concepts, edge cases, or a diagram when they help.

For historical motivation, use the method in the `why` skill.
