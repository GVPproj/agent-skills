# Personal agent skills

My trim of https://github.com/mattpocock/skills

These are simplified to my workflow, with some extra rules and edits (attempting) to counteract bad design habits in the models.

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

All skills also have native Pi commands, such as `/skill:setup` and `/skill:tdd`. The short commands are thin prompt templates that read the skill files.

### Supporting skills

These are available to the agent but have no additional short aliases to remember:

- **grilling**: the interview discipline behind both grill commands.
- **domain-modeling**: shared domain language, concrete business scenarios, glossary formats, and selective ADRs.
- **codebase-design**: deep modules, interfaces, seams, adapters, and testability; used by TDD when the interface needs design work.

They are ordinary editable skills in `skills/`. Invoke them explicitly with `/skill:domain-modeling` or `/skill:codebase-design` when useful.

## Project configuration

`/setup` previews changes, asks for confirmation, then records the tracker and domain-document conventions in the project's `docs/agents/` and effective Pi context file. GitHub, GitLab, local Markdown, and a user-described tracker such as Linear are supported. Credentials stay outside these documents.

