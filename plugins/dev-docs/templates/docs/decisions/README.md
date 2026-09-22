# Decision records

One file per decision: `YYYY-MM-DD-short-slug.md`.

Diffs already record *what* changed. These record *why*, which is the part
that's expensive to reconstruct and the part that stops someone undoing a
deliberate choice six months later because it looked like an accident.

**Write one when:** you picked between real alternatives, chose a dependency,
set a boundary, or deliberately did something that looks wrong without context.

**Don't write one when:** there was only one sensible option, or the reasoning
is obvious from the code. Ceremony for its own sake makes people stop reading
the folder.

These are historical. Don't edit an old one to match new reality; write a new
one and mark the old superseded.

## Template

```markdown
# YYYY-MM-DD — <short title>

**Context:** what situation forced a choice
**Decision:** what we chose
**Why:** the reasoning, in 2–5 lines
**Rejected:** alternatives considered and why not
**Status:** accepted | superseded by <file>
```
