# Architecture

<!-- How the system is put together, in prose. Not an inventory.

     KEEP OUT of this file: class lists, file trees, full dependency lists,
     function signatures. If a tool could generate it, it doesn't belong here.

     Delete any section that doesn't apply. -->

## Overview

<!-- Two or three sentences: the shape of the thing. A reader should be able to
     stop here and still have a rough mental model. -->

## Components

<!-- The major pieces and what each is responsible for. One short paragraph
     each. Name the piece, say what it owns, say what it deliberately doesn't.

     Examples of a "piece": a subsystem, a service, a layer, a module.

     **Renderer** — the only thing that touches the graphics API. Anything
     that needs to draw submits to it. Knows nothing about game rules.
-->

## Data

<!-- DELETE IF THERE IS NO PERSISTENT DATA.

     What is stored, where it lives, and what shape it's in at a conceptual
     level. Not a schema dump; the schema is in migrations. The useful content
     is things like "user state is the source of truth, everything else is
     derived" or "saves are a single JSON file, no migrations yet". -->

## External dependencies

<!-- DELETE IF THE SYSTEM TALKS TO NOTHING EXTERNAL.

     Third-party services, APIs, auth providers, anything you'd be broken
     without. For each: what it does for you, and what happens when it's
     unavailable. Libraries belong in the package manifest, not here. -->

## Boundaries

<!-- The rules about what may not talk to what, and why. This is the section
     that actually prevents bad merges, because it's the part a newcomer
     cannot infer from reading one file.

     "Player never talks to Renderer directly."
     "Nothing outside the data layer writes to the database."
-->

## Known rough edges

<!-- DELETE IF NONE.

     Places where the real system doesn't match the ideal, and you know it.
     Being honest here beats a reader discovering it at 2am. Anything with a
     fix planned should be a GitHub issue; link it. -->
