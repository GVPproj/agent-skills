# Upstream provenance and local changes

Source: https://github.com/mattpocock/skills

Copied revision: `59db609eb1e18aaf59b63284d0e52255aff0c63c`

Pinned source: https://github.com/mattpocock/skills/tree/59db609eb1e18aaf59b63284d0e52255aff0c63c

The upstream MIT license and copyright notice are retained in `LICENSE`.

## Included directories

From `skills/productivity/`:

- `grill-me`
- `grilling`
- `handoff`

From `skills/engineering/`:

- `grill-with-docs`
- `implement`
- `tdd`
- `to-tickets`
- `code-review`
- `prototype`
- `setup-matt-pocock-skills` → local `setup`
- `diagnosing-bugs`
- `codebase-design`
- `domain-modeling`

Copied all supporting Markdown and the debugging script. Omitted `agents/openai.yaml` files, which are Codex UI metadata, not Pi sub-agent definitions. Did not copy the upstream plugin, package tooling, other skills, or repository-specific agent instructions.

## Local adaptations

1. Flattened the selected skills into `skills/`; renamed setup and its references to `setup`.
2. Replaced unavailable `Skill` tool calls with explicit reads of sibling `SKILL.md` files. Handoff now recommends Pi commands and file paths.
3. Adapted code-review's orchestration to the installed `subagent_spawn` / `subagent_wait` tools, with read-only reviewers and an explicit fallback if tools are missing.
4. Added work-in-progress scope to code-review. Upstream `implement` requests review before committing, but upstream review's `...HEAD` diff excludes uncommitted work. The local mode includes tracked worktree changes and explicitly checks relevant untracked source files. Committed-only mode is unchanged.
5. Made tracker triage labels optional in to-tickets and the local-tracker template. Upstream setup already skips label configuration without the optional `triage` skill; this avoids requiring configuration it never creates.
6. Setup edits the effective Pi context file, including `AGENTS.override.md`, instead of preferring a potentially shadowed `CLAUDE.md`.
7. Clarified that the debugging HITL script requires a human terminal, not Pi's non-interactive shell/background tools.
8. Added a local Pi package manifest, ten short prompt aliases, and ownership/editing documentation.
9. Added conditional web UI guidance to `implement`, preferring web standards and native browser primitives over new specialized libraries.
10. Added UI-testing guidance to `tdd`: test behavior and meaningful states using semantic roles or stable identifiers, rather than coupling tests to incidental copy or broad content snapshots.

The original templates still mention optional, uninstalled skills such as `triage`, `wayfinder`, `to-spec`, and `improve-codebase-architecture`. Those are explanatory integrations, not required dependencies. Retained them to avoid gratuitous template rewrites.

No DDD additions, wholesale testing-policy rewrite, or commit-policy changes were made. In particular, upstream implementation and prototype commit behavior remains; see README before use.

## Updating intentionally

Treat upstream as reference material, not a managed dependency. Compare a desired upstream revision against the pinned revision and selectively apply changes to your files. Do not run an upstream skill installer over this directory: it can overwrite your refinements. Update this record when intentionally importing changes.
