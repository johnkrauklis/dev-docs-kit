---
description: List problems noticed on this branch that are outside task scope, and file the ones I approve.
---

List every problem you noticed on this branch that is outside the task scope.
For each: one-line summary, file:line, suggested label (bug, design, or
tooling).

Then ask which to file. For each one I approve:
1. Search for duplicates first: `gh issue list --search "<key terms>"`. If a
   match exists, link it instead of creating a duplicate.
2. Otherwise `gh issue create` with a short title, the file and line, what's
   wrong, the current branch name, and the approved label.

Never create an issue without my explicit approval of that specific item.
