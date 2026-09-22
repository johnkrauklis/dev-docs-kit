---
description: Draft architecture.md and conventions.md by reading an existing, unfamiliar codebase.
---

You're being dropped into a codebase you haven't seen before, to draft its
initial docs from what's actually there. This is for onboarding an existing
project, not a scaffold-only setup — use `/dev-docs:setup-docs` first if
`docs/overview/` doesn't exist yet, then run this to fill in real content.

## What this does and doesn't do

You can observe what the code does and how it's organized. You cannot know
why a choice was made, what alternatives were rejected, or what the project
is trying to achieve — that context either lives in a person's head or it's
gone. So:

- **architecture.md and conventions.md**: draft these. Both are things a
  careful reader can infer from the code itself.
- **project-context.md**: do not draft this. Leave it as the stub, or if it
  already has content, don't touch it. Tell me at the end that this doc
  needs a human, and ask the questions its stub headers pose (what is this,
  who's it for, current phase, goals, constraints, non-goals) directly, in
  chat.
- **decisions/**: do not write decision records from code alone. If you spot
  something that looks like a deliberate, non-obvious choice (an unusual
  dependency, a pattern used inconsistently on purpose, a workaround), name
  it as a candidate and ask whether the reasoning is known and worth
  recording — don't guess at the "why" yourself.

## Never overwrite real content

Before drafting anything, check whether docs/overview/architecture.md and
docs/overview/conventions.md already exist and look like real content rather than the
empty template (a file under ~15 lines with mostly HTML comments and no
prose in a section is template, not content). For a template or missing
file, draft into it. For a file with real content already, don't touch it —
tell me what you found that looks inconsistent with the current code instead
of silently rewriting someone's doc.

## How to read the codebase

Scale the read to the codebase's size — for a large repo, sample rather than
reading every file:

1. Get the shape first: list the directory tree a few levels deep, read any
   existing README, check the package manifest or build config (package.json,
   CMakeLists.txt, pyproject.toml, etc.) for the language, framework, and
   real build/run/test commands.
2. Read entry points (main(), index files, app setup) to find the major
   pieces and how they're wired together.
3. Sample a handful of files per apparent subsystem — enough to describe
   what it's responsible for and how it talks to its neighbors, not enough
   to enumerate every class or function.
4. Look for a formatter or linter config to ground conventions.md in what's
   actually enforced, not guessed.

## Draft architecture.md

Follow the structure and rules already in docs/overview/architecture.md's template
(keep only sections that apply, no class lists or file trees, prose not
inventory). Write:

- **Overview**: two or three sentences, the shape of the thing.
- **Components**: the major pieces you actually found, one paragraph each —
  what each owns, what it doesn't. Only pieces you have real evidence for.
- **Data / External dependencies**: include only if the code actually has
  persistent storage or talks to something external. Say what you observed,
  not what you'd expect.
- **Boundaries**: rules you can see the code actually follow — e.g. "only
  the renderer imports the graphics library" — not aspirational rules.
- **Known rough edges**: things where the real code doesn't match what its
  own structure implies it should do. Only include what you're confident
  about; a wrong guess here is worse than leaving it out.

Never enumerate individual source files. Describe each component by its
role. At most, name one representative file or folder so a reader knows
where to look.

### Split into topic files if architecture.md would be long

If the drafted content would push docs/overview/architecture.md past roughly
150 lines, split it by concern instead of writing one long file: keep Overview,
Components, and Boundaries in architecture.md, and move Data and External
dependencies into their own files (docs/overview/data.md,
docs/overview/external-dependencies.md) if either section is substantial on
its own. This is a prose-organization choice, not a new kind of content —
every file this produces is still something you drafted and I confirmed, not
generated inventory. Say which files you're proposing before writing, since
this changes docs/overview/README.md's file table too.

Do not create separate files for a class list, file tree, or dependency
graph. That content is explicitly out of scope for this command — see "What
this doesn't do" below.

## Draft conventions.md

Fill in Commands from the actual build/run/test/format commands you found.
For Naming, File layout, and Style, only record patterns you can point to
in at least two or three places — a pattern used once isn't a convention,
it's a coincidence, and recording it as a rule will mislead the next person.

Describe patterns you observed, not rules for others to follow. If a pattern
could be a deliberate standard or could just be habit, mark it "Needs team
confirmation" instead of telling people to match it. Only link to other docs
you've confirmed exist in the repo. When linking to a doc outside
docs/overview/ (elsewhere in docs/, or the project's own README), use a
relative path from docs/overview/, like `../content-architecture.md`.

## What this doesn't do

This command drafts prose docs from what the code shows. It does not
generate a class diagram, dependency graph, or file-tree inventory, even
though those are also things a tool could pull from code. That's a
deliberate line, not an oversight: content like that goes stale within days
and looks authoritative right up until it's wrong, which is worse than not
having it. If a project genuinely needs that, it belongs in a separate,
CI-regenerated pipeline under docs/generated/ — not something drafted once
by hand here. Don't propose writing one; if asked, say so and point back to
this note.

## Self-check: no file-listing sentences

Never enumerate individual source files (see above) — but drafting under
that rule slips easily, so run this check yourself before showing me
anything, every time you draft or revise:

1. Scan every sentence in the drafts for source-file names (anything
   ending in a code file extension, or an obvious filename pattern).
2. If a sentence names more than one source file, rewrite it to describe
   those files by role or subsystem instead, naming at most one of them as
   a representative example.
3. Re-scan the rewritten draft until no sentence names more than one
   source file.

  - bad: "simulation.cpp plus ecology, flora, forestry, soil, cave..."
  - good: "simulation.cpp plus one file per gameplay subsystem"

Do this silently as part of drafting — don't narrate the check, just apply
it — and only then move to presenting the drafts below.

## Present before writing

Show me the full drafted text for each file. In that same response, after
the drafts and before asking for confirmation to write, always do both of
the following:

1. Ask the project-context.md questions directly, in chat (what is this,
   who's it for, current phase, goals, constraints, non-goals).
2. List any decision candidates you noticed, for me to confirm or reject.

Asking for confirmation to write without doing both of those first is
incomplete — don't do it. Do not write to disk until I confirm. If I ask for
changes, revise and show again before writing, still including both of the
above.

## Finish by

Once I confirm and you've written the files, confirm which files you
drafted vs. left untouched and why.