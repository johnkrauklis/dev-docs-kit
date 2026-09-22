---
description: Check open GitHub issues against the default branch and propose closing the ones that look resolved.
---

Check which open GitHub issues are already resolved on the default branch.

## Step 1: Confirm you're on the up-to-date default branch

Get the default branch name with:
`gh repo view --json defaultBranchRef -q .defaultBranchRef.name`

Compare it to `git branch --show-current`. If they differ, stop and tell me
to switch to the default branch first. Branches are where work happens, but
an issue only counts as fixed once the fix is on the default branch.

Then run `git fetch` and check whether the local default branch is behind
origin. If it is, stop and tell me to `git pull` first, so you're not judging
issues against stale code.

## Step 2: Read the open issues

Run `gh issue list --state open --json number,title,body,labels,url`.
If there are none, say so and stop.

## Step 3: Check each issue against the current code

For each issue, read the title and body, then find and read the actual code
or docs it describes. Don't judge from the title alone.

Also check for merged PRs that mention the issue number:
`gh pr list --state merged --search "<number>" --json number,title,url`
A merged PR that mentions the issue is supporting evidence, not proof. The
code is the proof.

Sort each issue into one of three groups:

- Looks resolved: the problem described is no longer present in the code.
  State the specific evidence, and link the PR that fixed it if you found one.
- Still open: the problem is still present. One line is enough.
- Can't tell: the issue is vague, refers to something you can't find, or
  needs a human judgment call. Say why rather than guessing.

## Step 4: Propose, then wait

Show all three groups together. For each "looks resolved" issue, show the
exact command you'd run:
`gh issue close <number> --comment "<evidence, and PR link if known>"`

Do not run any of them until I say which to close. Never close an issue I
haven't explicitly approved.

## Scope

This command only reviews and proposes closing existing issues. It doesn't
file new issues (that's /dev-docs:issues) or edit docs (that's
/dev-docs:docs-check).
