# docs/

Four things live here. Keep them short. A doc nobody trusts is worse than no doc.

| File | Answers |
|---|---|
| `project-context.md` | What are we building and why? |
| `architecture.md` | How is it put together? |
| `conventions.md` | How do we write code here? |
| `decisions/` | Why did we choose this over that? |

**Two rules.**

1. **Don't write down anything the code already says.** No class lists, file
   trees, function signatures, or dependency lists. Those go stale in a week
   and the code is the truth anyway. Write the things a reader can't get from
   reading the code: intent, boundaries, and reasoning.
2. **Update these in the same PR as the code that made them wrong.** Run
   `/docs-check` before opening a PR. There is no separate sync step.

Delete any section below that doesn't apply to this project. An empty heading
is a small lie.
