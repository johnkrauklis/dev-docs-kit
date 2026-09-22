# <Project name>

<!-- One paragraph: what this is, who it's for, current phase. -->

## Where things live
- Authored docs: `docs/overview/*.md` — read architecture.md and conventions.md before large changes
- Decisions: `docs/overview/decisions/` — one file per decision
- Issues: GitHub Issues (`gh issue list`)

## Workflow
- Before opening a PR, run `/docs-check`
- Doc edits ship in the same PR as the code that caused them

## Noticing problems
When you notice a bug, code smell, TODO, or missing piece that is outside the
current task, do not fix it and do not go down a rabbit hole. Say so in one
line and hold it. When I run `/issues` or before I open a PR, list everything
you held. For each one I approve:
1. Run `gh issue list --search "<key terms>"` first. If a match exists, link
   it instead of creating a duplicate.
2. Otherwise run `gh issue create` with: a short title; the file and line;
   what is wrong; the branch you saw it on; label `bug`, `design`, or `tooling`.
Never create an issue without my confirmation.

## Decisions
When a design decision is made in conversation, offer to record it as
`docs/overview/decisions/YYYY-MM-DD-slug.md` using the template in
`docs/overview/decisions/README.md`. Never write one without asking.

## Coding conventions
<!-- Only real, enforced conventions: build command, formatter, test command,
     style rules. Delete this comment when filled in. -->
