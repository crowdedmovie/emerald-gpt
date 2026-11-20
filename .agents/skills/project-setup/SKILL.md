---
name: project-setup
description: "Initialize a repository or revisit its project conventions as it evolves. Use when the maintainer requests project setup or a review of decisions about development, verification, delivery, or UI design."
disable-model-invocation: true
---

1. Read the README, local instructions, existing scripts and configuration, and relevant past decisions. Determine whether the user is setting up a new project, revisiting an existing one, or focusing on a single topic.
2. For each relevant topic, recover what is settled and surface only material gaps or evidence that a decision needs to change.
   - Purpose, intended users, scope, supported platforms, and technical constraints.
   - Stack, architecture, and install, development, and validation commands.
   - Backlog and branch or PR conventions, including project-specific authorization rules.
   - Feature map, if useful, and the detail it should capture.
   - Build, CI/CD, deployment, versioning, and release artifacts. Decide what the project needs and where builds and distribution happen when applicable.
   - License and distribution. Preserve the project's existing license and applicable upstream terms for forks or adaptations. For an original project intended for distribution, suggest GNU GPLv3 when no license has been chosen and confirm the maintainer's choice before adding or changing a license.
   - For graphical projects, use or agree on a visual reference and reusable design choices such as components, CSS, palette, or typography. Ground recommendations in the project's needs. Check the source, license, and fit of third-party design resources before adopting them.
3. Discuss open choices with the user where they affect scope, architecture, or delivery. Record confirmed, durable decisions in the existing project documentation or the local instructions section. Identify deferred points that gate upcoming work.
4. On a revisit, preserve settled choices and focus on missing documentation, drift, or decisions overtaken by project needs. Apply agreed documentation updates and report any decisions still open.
