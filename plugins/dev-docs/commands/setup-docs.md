---
description: Scaffold docs/, decision records, PR template, and GitHub labels into the current repo.
---

Set up the dev-docs structure in the current repo. Do this in order, checking
your work at each step rather than assuming it succeeded.

## 1. Confirm you're at a repo root

Run `git rev-parse --show-toplevel` and confirm the current directory matches.
If it doesn't, or the command fails, stop and tell me — don't guess a path or
create files anywhere else.

## 2. Copy the templates, never overwriting

The plugin's templates live at `${CLAUDE_PLUGIN_ROOT}/templates/`. For each
file below, copy it from there to the repo path shown, but only if the repo
path doesn't already exist. If it exists, skip it and tell me at the end
instead of overwriting — I may already have real content there.

- `templates/docs/README.md` → `docs/README.md`
- `templates/docs/project-context.md` → `docs/project-context.md`
- `templates/docs/architecture.md` → `docs/architecture.md`
- `templates/docs/conventions.md` → `docs/conventions.md`
- `templates/docs/decisions/README.md` → `docs/decisions/README.md`
- `templates/github/pull_request_template.md` → `.github/pull_request_template.md`

## 3. Handle CLAUDE.md specially

Never overwrite an existing `CLAUDE.md`. If one exists, copy the template to
`CLAUDE.md.new` instead and tell me to diff and merge it by hand — the
existing file may have real project-specific content (build commands, style
rules) that would be lost otherwise. If no `CLAUDE.md` exists, copy the
template straight to `CLAUDE.md`.

Template: `templates/CLAUDE.md`

## 4. Create the three labels

Run, tolerating "already exists" errors silently:
```
gh label create bug
gh label create design
gh label create tooling
```
If `gh` isn't installed or isn't authenticated, tell me to create the three
labels by hand instead of failing silently.

## 5. Report a summary

List what was created, what was skipped because it already existed, and what
needs my manual attention (CLAUDE.md.new, missing gh). Don't just say "done."

## 6. Suggest next steps

Tell me to:
- Fill in `docs/project-context.md`, `docs/architecture.md`, and
  `docs/conventions.md` with real content, deleting sections that don't apply
- Merge `CLAUDE.md.new` into `CLAUDE.md` if that file was created
- Run `/docs-check` before my first PR through this workflow
