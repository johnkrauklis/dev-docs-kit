---
description: Check whether this branch's changes make any authored doc inaccurate, before opening a PR.
---

If `$ARGUMENTS` names a branch, use it as the base branch for this check.
Otherwise, detect the repo's default branch:
`gh repo view --json defaultBranchRef -q .defaultBranchRef.name`
If `gh` isn't available, fall back to checking whether `main` or `master`
exists locally and use whichever one does.

Compare this branch against the base branch (`git diff <base>...HEAD`;
if there are no commits yet, use the working tree diff instead).

For each authored doc in docs/*.md (ignore docs/decisions/):
1. State whether the diff makes any part of it inaccurate or incomplete.
2. If yes, propose the specific edit as a diff. Do not apply it until I confirm.
3. If a design decision was made on this branch that isn't recorded, propose a
   decision record (see docs/decisions/README.md) and ask before writing it.

Be conservative: only flag real inaccuracies, not things that "could be
mentioned." A doc that is unaffected by this diff should get a one-line
"no change needed," not a suggestion to expand it.

## Step: Check for an issue this branch fixes

Run `gh issue list --state open` and see if any open issue looks like it's
fixed by this branch's changes. If one looks like a match, remind me to
include `Closes #<number>` in the PR description so GitHub closes it
automatically on merge.
