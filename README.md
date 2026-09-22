# dev-docs-kit

A Claude Code plugin that replaces a shared external doc/issue tool with docs
that live in the repo and are checked at PR time.

Works for any codebase — a game, a service, a script. Nothing in it is
project-specific; the project-specific content is what you fill into the
templates after setup.

## What it does

- `/setup-docs` — scaffolds `docs/`, decision records, a PR template, and
  three GitHub labels into the current repo. Never overwrites existing files.
- `/docs-check` — before opening a PR, diffs your branch against main and
  tells you which authored docs your change made inaccurate. Proposes edits,
  never applies them without confirmation. Also catches undocumented design
  decisions.
- `/issues` — lists problems noticed during work that were outside the task's
  scope, then files the ones you approve to GitHub Issues (with duplicate
  checking).
- `/audit` — for dropping this into a codebase that already exists. Reads the code and drafts architecture.md and conventions.md from what it actually finds, shows you the draft before writing anything, and never touches a doc that already has real content. Doesn't guess at project-context.md or write decision records from code alone — it asks you instead, since "why" isn't something code can answer.
- `/review-issues` — checks open GitHub issues against the default branch and
  proposes closing the ones that look resolved. Never closes anything without
  approval.

## What it deliberately doesn't do

No database, no background watcher, no hooks that fire on every file edit, no
writes without asking first. If you stop using this tomorrow, you're left
with plain markdown in git and plain GitHub issues — nothing to migrate away
from.

## Install

Clone this repo once, then add it as a local-directory marketplace. This is
the documented method — `/plugin marketplace add` with a GitHub URL or
`owner/repo` shorthand has been unreliable (see note below), so don't rely on
it for now.

```
git clone https://github.com/johnkrauklis/dev-docs-kit.git
```

Then in Claude Code, from any project:

```
/plugin marketplace add /full/path/to/dev-docs-kit
/plugin install dev-docs@dev-docs-kit-marketplace
```

Use the full local path to wherever you cloned it. On Windows this looks like
`C:\Users\you\Projects\dev-docs-kit`; on macOS/Linux, `/home/you/dev-docs-kit`
or similar.

**To get updates later**, `git pull` inside your clone. A local-directory
marketplace loads in place, so Claude Code picks up the change without
re-adding anything.

> **Known issue:** `/plugin marketplace add <github-url-or-shorthand>` has
> failed on at least one machine with `fatal: Cannot prompt because user
> interactivity has been disabled`, even though a plain `git clone` of the
> same URL succeeds immediately. This looks like a bug in how Claude Code
> invokes git for that command, not a problem with this repo or your
> credentials. The local-path method above sidesteps it entirely. If it
> starts working reliably in a future Claude Code version, switch back —
> it's one fewer manual step.

## Set up a new project

In the project's repo, with Claude Code running:

```
/setup-docs
```

This creates the doc files, the PR template, and the three labels
(`bug`, `design`, `tooling`). It will not touch an existing `CLAUDE.md` —
if you have one, it writes `CLAUDE.md.new` instead so you can merge by hand.

Then:

1. Fill in `docs/project-context.md`, `docs/architecture.md`, and
   `docs/conventions.md`. Each file has HTML comments explaining what belongs
   there and, in `architecture.md`, which sections to delete if they don't
   apply (e.g. a game usually has no "External dependencies" section).
2. If `CLAUDE.md.new` was created, diff it against your existing `CLAUDE.md`,
   carry over any real conventions, then replace the old file.
3. Commit, and you're set up.

## Dropping into an existing codebase

If you're being handed a project that already has code but no `docs/`, run
`/setup-docs` first to get the folder structure and empty templates in
place, then run `/audit` to have it read the codebase and draft
`architecture.md` and `conventions.md` from what's actually there. It'll
show you the draft and wait for confirmation before writing anything, and it
will not draft `project-context.md` — that one it'll ask you about directly,
since intent isn't something it can read out of the code.

## Day-to-day workflow

1. Branch, make your change.
2. Before opening a PR: run `/docs-check`. Confirm or reject its proposed
   edits.
3. Open the PR using the template. Check the Docs checklist honestly.
4. If you noticed unrelated problems while working, run `/issues` to file
   them instead of fixing them mid-branch.
