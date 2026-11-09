---
name: to-pr
description: Publish completed changes on a fresh branch as one squashed commit, push it, and open a well-written pull request that closes the associated issue when present. Use when asked to send changes to PR or open a pull request.
---

# To PR

Turn the current work into a ready-for-review pull request. This command authorizes creating a branch, committing and squashing the intended changes, pushing that new branch, and opening the PR—not merging it or closing an issue immediately.

## 1. Establish scope

- Read the repository's agent instructions, contribution guide, PR template, and `docs/agents/issue-tracker.md` when present. Follow its branch, commit, testing, and tracker conventions. Do not require `/setup` just to publish a PR.
- Inspect the working tree (including staged and untracked files), remotes, current branch, recent commits, and existing PRs. Resolve the intended target repository, push remote, and base branch from the request, repository conventions, and remote metadata; do not assume `origin` or `main`.
- Identify the intended changes from the request and conversation, then inspect the full diff against the merge base with the target branch. Include existing commits as well as uncommitted work. If scope, base, remote, or ownership of changes is ambiguous, ask before changing history or publishing.
- Find any associated issue in explicit arguments, the conversation, branch name, or commit references. Read the actual issue and relevant comments; verify that the changes fulfill it. Do not invent an issue or treat a matching number as proof. If none is present, proceed without one.
- Check hosting CLI authentication and repository access before mutating Git state. If an existing PR already covers this work, report it and ask before creating a duplicate.

## 2. Verify readiness

Run the repository's relevant tests, lint, and other required checks. Inspect the diff for accidental files, secrets, generated noise, and unrelated changes. Do not stage indiscriminately with `git add .` or `git add -A`.

Fix only small, in-scope problems. For failing checks or substantial missing work, report the blocker rather than publishing a ready PR. Distinguish checks actually run from checks unavailable in this environment; ask before proceeding with missing required validation. Never claim CI passed just because local checks passed.

## 3. Create a fresh branch and squash

- Fetch the relevant remote refs and resolve the target base and merge base. Stop on an in-progress merge/rebase or unresolved conflicts. Confirm every commit and change to be included is in scope; do not squash unrelated work or commits already in the base.
- Always create a **new, uniquely named branch** for this invocation, even if currently on a feature branch. Use the project's naming convention, including the issue identifier when appropriate. Never commit to or rewrite the default, protected, shared, or original branch.
- Carry only the intended changes onto that branch. Stage explicit paths or hunks, preserving unrelated work. If unrelated working-tree/index changes cannot safely remain isolated during the squash, stop and ask; do not silently stash, discard, or commit them.
- Before rewriting commits, preserve the pre-squash committed tip with a local backup ref and record the original branch and relevant SHAs. Commit any intended uncommitted changes on the new branch first so the backup also protects that work.
- Squash the branch's complete intended delta from the merge base into **one meaningful commit**, using a noninteractive operation (for example, a soft reset to the verified merge base followed by a commit). Only do this with a clean index/worktree after the scoped changes are committed; otherwise stop to resolve isolation safely. Never use `reset --hard`, `clean`, or a force push.
- Verify the final tree is identical to the pre-squash tree, the diff contains exactly the intended changes, and `git rev-list --count <base>..HEAD` is `1`. If there is no net change, stop rather than publishing an empty PR. Keep the backup ref until success; report it if anything fails.

## 4. Push and open the PR

Push the new branch with an upstream to the verified remote. Use a normal push; on a name collision, choose a fresh name rather than overwriting a remote branch. Open a non-draft PR against the verified base with the host's supported CLI/API (for GitHub, `gh pr create` with explicit base, head, title, and a body file). Use a temporary body file to avoid shell interpolation problems.

Write for a reviewer, not as a transcript:

- **Title:** concise, specific, and outcome-focused; follow repository conventions.
- **Summary:** what changes and why, including the user-visible behavior or problem solved. Mention important design decisions only when useful for review.
- **Validation:** exact checks run and their outcomes. Clearly disclose anything not run.
- **Risks / follow-up:** include only meaningful limitations, compatibility concerns, or deployment requirements.
- **Issue:** when the PR fully resolves a verified issue, include the platform's supported auto-closing reference, such as `Closes #123` or a fully qualified GitHub issue URL. Use the configured tracker integration/convention for external issues such as Linear; do not pretend a plain URL guarantees automatic closure. If the issue is only partly addressed, use a non-closing reference and explain the remaining scope. Never close the issue directly before merge. Omit this section when there is no issue.

Honor the repository PR template rather than adding redundant headings. Avoid inflated claims, boilerplate, full commit logs, or invented test results.

## 5. Confirm delivery

Read back the created PR and verify its base, head, title, body, commit count, and issue reference. Report the PR URL, branch, and validation summary; flag any closure-integration limitation. If publication fails, report what succeeded and the recovery details without deleting work or retrying destructively.
