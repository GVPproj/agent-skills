---
name: quickie
description: "Implement a change directly, without tests, comments, builds, or ceremony. Use when the user explicitly asks for a quickie."
disable-model-invocation: true
---

Implement the user's request with the smallest appropriate change. Read only the context needed and follow the project's existing conventions. Ask only if a blocking ambiguity prevents implementation.

Do not add or run tests, add code comments, run builds, typechecks, or linters, or invoke planning, TDD, review, or PR workflows. Do not install dependencies or start servers just to verify the change.

For UI work, read and follow `../implement/ui.md` (relative to this skill directory). Keep its design, accessibility, and interaction guidance. Inspect and verify with available UI tools only if the UI is already running; skip any verification that requires tests, builds, installs, or starting a server. Mention skipped verification briefly.

Skip progress narration, elaborate summaries, and follow-up offers. Make the change, then give a brief completion note stating that checks were not run. Do not commit unless asked.
