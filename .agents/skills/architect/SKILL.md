---
name: architect
description: "Design a substantial feature, module boundary, or contract change before implementing it. Use when the shape of the code affects callers, ownership, or compatibility."
---

1. Trace the existing system and the behavior to preserve. Identify callers, ownership of state, integration constraints, and how the change will be verified.
2. Sketch from the caller's point of view. Show the key types, signatures, and module boundaries. Compare distinct options when the tradeoff could change the choice. Screen the proposed shape with [design red flags](references/design-red-flags.md).
3. Recommend a shape and explain its important tradeoffs. Keep material design decisions with the user as required by the project. If the request is for design only, hand over the sketch and verification plan.
4. When implementation is in scope, build against the sketch and verify from the intended entry point. Revisit the sketch if several callers need special cases or if implementation contradicts an ownership decision.
