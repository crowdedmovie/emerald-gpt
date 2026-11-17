---
name: clean-branches
description: "Audit or safely remove stale local Git branches in the current repository. Use only when the user explicitly requests a branch audit or cleanup, never after routine Git commands."
disable-model-invocation: true
---

1. **Scope and intent.** Work only in the Git repository containing the current working directory (`git rev-parse --show-toplevel`). Never scan sibling repositories or run periodically. An audit or dry-run request authorizes inspection only; a clear request to clean or delete obsolete branches authorizes deletion only under the conditions below. If intent is unclear, report candidates without deleting.
2. **Establish a reliable reference.** Prefer `origin` if configured, otherwise use the sole remote; if none or several ambiguous remotes exist, stop before deletion. Resolve its default branch from `git ls-remote --symref <remote> HEAD` rather than guessing `main` or `master`. Run `git fetch --prune <remote>`, and verify that `refs/remotes/<remote>/<default>` exists. If any remote check or fetch fails, report the problem and do not delete local branches. Pruning removes stale *remote-tracking references*, not local branches.
3. **Inspect local work.** Read `git status --short --branch`, `git worktree list --porcelain`, and `git for-each-ref --format='%(refname:short)%09%(objectname)%09%(upstream)%09%(upstream:remotename)%09%(upstream:remoteref)' refs/heads`. Identify the currently checked-out branches in **all** worktrees, not only the current directory. Never infer whether a branch was checked out in the past.
4. **Classify conservatively.** A branch is eligible only when **all** of these are true:
   - It is not the remote default branch, the current branch, or checked out in any worktree.
   - It has a configured upstream on the selected remote. After pruning, that remote-tracking ref is absent (`git show-ref --verify --quiet <upstream-ref>` fails), and `git ls-remote --heads <remote> <upstream-remoteref>` confirms the upstream branch is also absent on the server.
   - Its tip is fully contained in the fetched remote default branch (`git merge-base --is-ancestor <branch> refs/remotes/<remote>/<default>` exits successfully).
   Keep branches without an upstream, with existing remote branches, with unmerged commits, or with uncertain state. Squash-merged and rebased work may not pass ancestry checks: report those for manual review rather than assuming they are safe.
5. **Delete only on explicit cleanup requests.** Immediately before each deletion, recheck the candidate's object ID, upstream absence, ancestry, and all worktree attachments. Use `git branch -d -- <branch>` only. If Git refuses, retain the branch and explain why; never use `-D`, delete remote branches, switch worktrees, reset commits, or override Git safety checks.
6. **Report the result.** Name the repository and checked remote/default branch. List deleted branches and retained or uncertain branches with concise reasons, including fetch or deletion failures. If nothing qualifies, say so. Do not create a commit or PR merely for the cleanup.
