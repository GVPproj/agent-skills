# Personal agent skills

A small, locally owned Pi skills collection. These are editable source files; adapt them to your workflow.

## Use

Installed as a local Pi package at `~/agent-skills`. Run `/reload` in an existing Pi session, then run `/setup` **inside each project** to choose its tracker and documentation conventions.

| Command | Purpose |
| --- | --- |
| `/grill-me` | Interview about an idea or decision |
| `/grill-with-docs` | Interview while sharpening domain language and recording decisions |
| `/implement` | Implement a spec or tickets with testing and review |
| `/tdd` | Work test-first at agreed seams |
| `/to-tickets` | Publish approved vertical-slice tickets to the project's tracker |
| `/code-review` | Separate standards and specification reviews |
| `/simplify` | Audit for unnecessary code, comments, prose, and dependencies |
| `/prototype` | Explore logic/state or alternative UI designs |
| `/setup` | Configure the current project's tracker and domain documentation |
| `/diagnosing-bugs` | Diagnose with a tight, reproducible feedback loop |
| `/handoff` | Save a handoff for another session |

Arguments work normally, for example:

```text
/grill-with-docs redesign our subscription cancellation flow
/to-tickets turn the agreed plan into tickets
/implement .scratch/cancellation/issues/01-cancel-subscription.md
/code-review work-in-progress since HEAD, against .scratch/cancellation/spec.md
/simplify src/subscriptions
/handoff continue with the next ticket
```

All 14 skills also have native Pi commands, such as `/skill:setup` and `/skill:tdd`. The short commands are thin prompt templates that read the skill files; they do not duplicate the instructions.

### Supporting skills

These are available to the agent but have no additional short aliases to remember:

- **grilling**: the interview discipline behind both grill commands.
- **domain-modeling**: shared domain language, concrete business scenarios, glossary formats, and selective ADRs.
- **codebase-design**: deep modules, interfaces, seams, adapters, and testability; used by TDD when the interface needs design work.

They are ordinary editable skills in `skills/`, not hidden framework code. Invoke them explicitly with `/skill:domain-modeling` or `/skill:codebase-design` when useful.

## Edit your collection

Edit `skills/<name>/SKILL.md` and its adjacent reference files. Then `/reload`. For example:

```text
~/agent-skills/skills/implement/SKILL.md
~/agent-skills/skills/grilling/SKILL.md
~/agent-skills/skills/domain-modeling/SKILL.md
~/agent-skills/skills/codebase-design/SKILL.md
```

No build, dependency install, or publishing is needed. The local package loads these files directly.

The `prompts/` files only provide short command aliases. They assume this collection lives at `~/agent-skills`; if you move it, update those paths and reinstall the local package. Native `/skill:name` commands use Pi's discovered paths and do not depend on the alias paths.

## Project configuration

`/setup` previews changes, asks for confirmation, then records the tracker and domain-document conventions in the project's `docs/agents/` and effective Pi context file. GitHub, GitLab, local Markdown, and a user-described tracker such as Linear are supported. Credentials stay outside these documents.

By default there is one `GLOSSARY.md` and `docs/adr/`. Glossaries and ADRs are created lazily when there is something worth recording, not scaffolded empty. Multi-context layouts remain available for large projects. `triage` is not included, so its labels are optional and setup skips its label interview.

## Workflow defaults

- **Grilling asks a round of independent questions**, not necessarily one question at a time.
- **`implement` commits to the current branch** after testing and review. Change its final instruction if you prefer an approval gate or no commits.
- **`tdd` uses red → green**, with refactoring deferred to review, and requires agreement on seams before tests.
- **`prototype` can fold validated decisions into real code and commit a throwaway branch**, with a pointer on the implementation issue. It is not strictly read-only exploration.
- **`code-review` keeps standards and spec findings separate**, rather than producing one ranked list.
- **`handoff` writes to the OS temporary directory**, not the project; copy it elsewhere if you need durable storage.

Sub-agent workflows use the sub-agent tools provided by your existing Pi configuration. This package does not install an extension. Without those tools, independent parallel reviews/design exploration need another runner or an explicitly acknowledged sequential fallback. Git, tracker clients/MCP access, and project-specific test tools are needed only when the chosen workflow uses them.

## Domain-driven design

Keep both `domain-modeling` and `codebase-design`: the first clarifies the business model; the second shapes the software implementing it. Neither is a complete DDD methodology.

Put domain rules in `domain-modeling` (bounded contexts, invariants, ownership, and consistency needs), implementation guidance in `codebase-design`, and checks in `code-review`. Prefer project language and real business constraints over mandating aggregates, repositories, events, or extra layers everywhere.

## Install elsewhere / remove

Keep the default directory name to use the aliases unchanged:

```sh
pi install ~/agent-skills
# In Pi: /reload
```

To stop loading the collection without deleting your editable files:

```sh
pi remove ~/agent-skills
# In Pi: /reload
```

Do not also copy or symlink the skills into another auto-discovered directory; that can create duplicate names. Adding a new skill only requires `skills/<name>/SKILL.md`; add a matching prompt under `prompts/` if you also want a short alias.
