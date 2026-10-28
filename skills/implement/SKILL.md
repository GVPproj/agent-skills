---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

If the user passes a ticket reference, fetch it from the issue tracker and state its title before starting. If the reference is ambiguous, ask.

If the work includes any UI, read and follow `ui.md` (relative to this skill directory).

Read and follow `../tdd/SKILL.md` (relative to this skill directory) where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, read and follow `../code-review/SKILL.md` (relative to this skill directory) to review the work.

If the code-review surfaces changes to be made, tdd through them, then end with an offer commit your work to the current branch (don't commit automatically).
