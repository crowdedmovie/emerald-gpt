# Shared Agent Instructions

This AGENTS.md provides common development guidelines for AI coding agents across repositories. Follow the current repository's specific instructions and the user's explicit requests when they refine or override this baseline.

## 1. Working Principles

- Prefer simple, maintainable, reliable solutions over unnecessary complexity.
- Respect the existing architecture, technology stack, conventions, and intended platforms.
- Keep changes focused; avoid unrelated refactoring, premature abstractions, and needless dependencies.
- Make routine implementation decisions autonomously. Consult the user for material changes to requirements, architecture, supported behavior, or distribution.
- Do not impose a framework, build system, packaging, or deployment model unless the project's requirements justify it.
- Apply instructions proportionately to the repository. Not every project needs an application, automated tests, builds, deployment, or published versions.
- Do not request approval again for an action already explicitly authorized within the current task's scope.

## 2. Code Quality and Security

- Write clear, consistent code with meaningful names and focused functions.
- Keep business logic separate from presentation code when useful, without forcing extra layers.
- Follow existing formatting, typing, and linting conventions where applicable.
- Comment non-obvious decisions or logic, rather than narrating obvious code.
- Handle relevant errors and edge cases; preserve compatibility with supported environments.
- Prefer existing dependencies and built-in functionality when practical; update dependency declarations when needed.
- Never hardcode, commit, disclose, or transfer passwords, tokens, credentials, or private signing keys.

## 3. Proportionate Validation

- Validate changes according to their scope, dependencies, and risk.
- For UI-only changes, prioritize relevant interactions and visual rendering when tools permit.
- For backend changes, prioritize the modified logic and directly affected integrations.
- Add or update automated tests when they materially help verify behavior; do not require unit tests for every feature.
- Do not run a full application-wide test suite for every small edit unless the change, project rules, or risk warrants it.
- Local builds and artifact preparation may be performed to validate authorized work without separate release approval.
- Before publishing a release or distributing artifacts, follow project-specific validation requirements.
- Never report a test, build, or visual check as successful unless it was actually performed. Explain relevant limits.

## 4. Branches and Pull/Merge Requests

### Before starting work

- Inspect the current branch and working-tree changes before editing files.
- When remote access is available, check whether the branch has an associated PR/MR, whether it has already been merged, and whether it remains appropriate for the requested work.
- Do not assume a branch is suitable merely because it was used in an earlier session.
- If the branch appears merged, obsolete, or unsuitable, report the situation at the start and recommend a concrete next action before editing files.
- If remote branch or PR/MR status cannot be checked, state that limitation.

### Organizing work

- Do not commit directly on the repository's default branch unless the user explicitly authorizes it for a minor, low-risk change.
- Create dedicated branches for coherent workstreams when needed; do not create a branch for every prompt or minor change.
- Creating a new working branch is permitted as part of authorized development. Switching to another existing branch requires explicit user authorization unless already requested.
- Continue related work on a suitable active branch, including across sessions and agents. Update its existing PR/MR when appropriate.
- For an independent workstream, propose a dedicated branch from the updated default branch.
- For work depending on unmerged changes, explain the dependency and propose either continuing the existing branch or using a dependent branch and PR/MR.
- Prefer the simplest branch arrangement that keeps the work reviewable. Do not introduce dependent PRs/MRs without the user's agreement.
- Do not automatically create a PR/MR at the end of every task.
- When a workstream is ready for integration, prepare or update its PR/MR for the user's review. Do not open a premature PR/MR merely because an agent session is ending.

### User control

- Never merge a PR/MR or enable auto-merge without explicit user authorization.
- Never delete branches, force-push, rewrite shared history, or discard unrelated changes without explicit user authorization.
- Authorization may be given in the initial task request; do not ask again for the same action within the approved scope.
- Respect existing branch protection and repository rules.

## 5. Commits and Attribution

- Commit at meaningful development milestones, grouping logically related changes together.
- Do not make a commit per file, per trivial adjustment, or automatically after every agent response.
- Avoid both excessive micro-commits and large commits that mix unrelated changes.
- Use clear, concise commit messages; prefer Conventional Commit prefixes where useful.
- Preserve the Git author and committer identity configured in the environment; do not impersonate the repository owner.

### AI co-authorship

- Add the applicable AI co-author trailer whenever an agent writes or modifies content included in the commit, including code, configuration, or documentation, regardless of the change's size or significance. Determine attribution by the contributing model's family, regardless of the editor, orchestrator, API provider, or execution environment.
- Use the following trailers:

  | Model family | Trailer |
  | --- | --- |
  | OpenAI | `Co-authored-by: Codex <noreply@openai.com>` |
  | Anthropic / Claude | `Co-authored-by: Claude <noreply@anthropic.com>` |
  | Google / Gemini | `Co-authored-by: Gemini <218195315+gemini-cli@users.noreply.github.com>` |

- For other model families, do not add an AI co-author trailer.
- Use reliable session or runtime information to identify the model family. Do not infer it solely from the tool's name or invent an identity.
- If the model family cannot be established reliably, omit the AI co-author trailer.
- Add each applicable trailer once, separated from the commit message body by a blank line.
- Preserve legitimate existing co-author attributions. Do not claim credit for work the current agent did not contribute to.

### Signing

- Use the environment's existing Git commit-signing configuration when available.
- Do not disable signing merely to work around a signing error.
- Never export or upload private signing keys to a cloud environment.
- When signing is unavailable, clearly report that commits are unsigned; do not claim Verified status.

## 6. Versioning and Releases

- During project initialization, determine whether the project is expected to publish versions. Revisit this decision when distribution needs change.
- For projects that publish versions, use Semantic Versioning with Git tags named vMAJOR.MINOR.PATCH, unless an existing project convention or explicit instruction requires otherwise.
- Do not introduce version numbers, tags, or release procedures for projects that do not need them.
- Development does not need a release from the start. Prefer v0.1.0 for the first usable release that meaningfully fulfills the project's initial purpose.
- Continue normal development through as many commits, tasks, and PRs/MRs as appropriate between releases.
- Do not create a version bump, tag, or release just because a task or PR/MR was completed.
- After v1.0.0, use PATCH for compatible fixes, MINOR for compatible new functionality, and MAJOR for breaking changes to supported public behavior or interfaces.
- In 0.x, treat versions as pre-stable and adjust increments to the project's maturity and impact.
- At significant milestones, consider whether the changes since the latest release justify a new publication.
- When proposing a release, inspect those changes and explain the suggested version, meaningful features and fixes, readiness, validation needs, and required artifacts. Recommending that the project wait is also acceptable.
- Creating release tags, publishing releases, distributing release artifacts, or changing a published version requires explicit user authorization.
- A request to perform a release may authorize the complete workflow from preparation through publication. Do not request the same authorization again unless the scope materially changes.
- Once authorized, follow repository-specific release checks and procedures. Keep published version tags stable and traceable to the released commit.
- Publish concise release notes on the hosting platform. Do not require a separate CHANGELOG.md unless the repository benefits from one.

## 7. Documentation and Backlog

### Documentation

- Keep documentation short, accurate, and useful.
- Update the README and related instructions when changes affect users, installation, configuration, or operation.
- Record important assumptions, non-obvious behavior, and known limitations.
- Keep executable procedures in scripts or appropriate tooling; reference them from AGENTS.md rather than embedding lengthy instructions.
- Do not create unnecessary documentation files.

### Backlog

- Use BACKLOG.md as the repository's reference for future features, improvements, and deferred work.
- Create it when there is something to record and link to it from the README.
- When the user asks to retain an idea for later, record it without starting its implementation.
- Check for an existing entry before adding one.
- Keep entries concise: describe the need, intended behavior, and meaningful open questions. Add acceptance criteria when preparing the work for implementation.
- Clearly distinguish unresolved ideas from work approved for implementation.
- A backlog entry is not authorization to implement it.
- Remove an entry once the work has been integrated into the project's reference branch, normally the default branch. For partially completed work, retain only the remaining scope.
- Use Git history and PRs/MRs to preserve completed-work history rather than accumulating completed entries in the backlog.

## 8. Continuity and Agent Coordination

- Treat repository files, Git history, and existing PR/MR discussions as durable context. Do not assume access to earlier conversations or another agent's memory.
- Before continuing existing work, inspect relevant changes and decisions rather than relying only on a previous summary.
- Preserve changes made by the user or other agents. Do not overwrite, revert, or clean up unrelated work.
- For long-running or interrupted work, leave enough context in the existing tracking or documentation location to resume: objective, current state, important decisions, validations performed, blockers, and next action.
- Do not create a separate hand-off document for every small task.
- If multiple agents work concurrently, define clear task boundaries and integration responsibility.
- Prefer separate worktrees or branches for independent concurrent changes. Coordinate explicitly before modifying shared files.
- Review and validate delegated changes in the integrated result before considering the work complete.

## 9. Reporting and Hand-off

- Briefly summarize changes made, relevant validations actually performed, and known issues or unfinished work.
- State the current working branch and PR/MR status when relevant.
- Distinguish work implemented on a branch from work merged or released.
- Explain blockers and recommend concrete next actions when user input is needed.
- Point out meaningful next decisions, including a potential release when warranted, without turning every task completion into a PR/MR or release request.

## 10. Project Initialization and Repository-Specific Instructions

When starting a new project, inspect the existing repository and resolve the relevant unanswered questions with the user:

- Purpose, intended users, initial scope, and explicit exclusions.
- Supported platforms, execution environments, and technical constraints.
- Existing stack or technical choices that need to be made.
- Installation, development, and validation commands.
- Backlog location and branch/PR conventions.
- Whether the project needs published versions, release artifacts, or deployment.
- Project-specific authorization requirements and exceptions.

Do not repeat this initialization at every session. Reuse recorded decisions and revisit them only when requirements change.

Not every question must be settled before development begins. Record unresolved points when useful and resolve them before work that depends on them.

Add confirmed, durable repository-specific instructions below or in appropriately scoped AGENTS.md files. Reference detailed documentation instead of duplicating it.

Update these instructions when lasting project conventions change. Keep transient task progress, feature ideas, and session history in their appropriate tracking locations.

### Repository-Specific Instructions

Add only information relevant to this repository. Omit unused sections and avoid speculative commands or requirements.
