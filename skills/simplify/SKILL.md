---
name: simplify
description: "Audit a plan, diff, file, directory, or codebase for dead code, stale comments, inflated prose, and underused dependencies. Propose reductions and apply only approved changes. Use when the user asks to simplify, clean up unnecessary baggage, or find things to remove."
---

# Simplify

Audit for unnecessary baggage and propose reductions. Report first; apply nothing without approval. This is independent of `code-review`, and can cover existing code as well as changes.

## Steps

1. **Set the scope.** Use the target the user gives: a plan, diff, file, directory, or whole codebase. If the scope is unclear, ask. For a whole-codebase audit, first map the file tree, entry points, dependencies, and usage. Inspect outside the target when needed to establish usage or impact, but keep proposals within the agreed scope.
2. **Hunt for baggage:**
   - **Dead code:** unused files, exports, functions, imports, configuration, and dependencies. Check callers, scripts, tests, dynamic loading, framework conventions, and public APIs before calling something unused. A search with no matches is not proof of no external consumers.
   - **Archaeological comments:** comments about obsolete implementations, completed migrations, or behavior that no longer exists. Keep explanations of why current behavior exists, including non-obvious constraints.
   - **Inflated or generic prose:** awkward, repetitive, overly formal, or AI-sounding language in comments and docs. Quote the text and suggest a clear, concise alternative. Judge the wording, not whether an AI wrote it; preserve useful meaning and project terminology.
   - **Underused dependencies:** identify actual uses and evidence of size or other cost. Consider whether a small bespoke implementation would really reduce complexity, weighing correctness, security, compatibility, maintenance, and replacement tests. One use alone is not enough; avoid casually replacing security-sensitive or subtle functionality.
3. **Report proposals.** For each item, give the location, evidence, proposed removal or reduction, and what would be lost or put at risk. For prose, include the original and suggested wording. State uncertainty and checks still needed; do not present an unverified candidate as safe to delete. For a large or whole-codebase audit, group by area and rank safe, high-value cuts first. If there are no supported candidates, say so.
4. **Stop and ask** which proposals to apply. Do not edit during the audit, even if the user asked to simplify. Approval of one item is not approval of the rest.
5. **Apply approved changes** in small batches. Run relevant tests, builds, or other checks after each batch; report commands and results. If a check fails, stop and report before continuing. If verification is unavailable, say what was not checked and why.

## Must not

- Remove something merely because it is unfamiliar or a search found no references. If usage is uncertain, leave it and say what needs checking.
- Rewrite working code for style alone, or expand the scope into a general refactor. Small replacement code is acceptable when it removes more complexity than it adds.
- Remove comments that explain current intent, constraints, or domain decisions merely because they are old.
- Touch generated files, vendored code, or lockfiles during the audit. When an approved dependency change requires a lockfile update, use the project's package manager and include that update in the approved batch.
- Apply unapproved proposals or continue to the next batch after a failed check.

## Example output

> **Can be less:**
> 1. `src/legacy.ts` — no references found in source or scripts; check external consumers before deleting. Risk: an undocumented public import could break.
> 2. `src/cache.ts:42` — comment describes a removed migration; delete it. Lose: obsolete history only.
> 3. `docs/setup.md:18` — “seamlessly leverage the robust configuration ecosystem” → “configure the tool”. Lose: no technical detail.
> 4. `package.json`: `example-lib` — used once for a small formatting task; compare bundle impact and edge cases before replacing it. Risk: a bespoke version may miss supported formats.
>
> Which should I apply?
