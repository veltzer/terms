# terms

Shared technical-terms registry used across veltzer documentation projects
(`teaching-syllabi`, `teaching-slides`, etc.).

## Layout

- `terms.single_meaning/` — terms that unambiguously refer to a technology
  and SHOULD be wrapped in backticks in prose
  (e.g. `Python`, `Kubernetes`, `Apache HTTP Server`).
- `terms.ambiguous/` — terms that collide with common English words and
  MUST NOT be wrapped in backticks
  (e.g. `Apache`, `Spring`, `Go`, `find`, `Agile`).

A term must appear in exactly one of the two registries. Files within each
directory are split by topic for readability — the consumers concatenate
them at load time.

## Consumers

Each consuming project syncs this repo into local `terms.ambiguous/` and
`terms.single_meaning/` directories, typically via a sync script that runs
`git clone --depth 1` and copies the two folders.

The `rsconstruct` `terms` checker reads these to enforce backticking
conventions in markdown source.

## Editing

- Add unambiguous proper-noun product names to `terms.single_meaning/`.
- Add anything that overlaps with English to `terms.ambiguous/`.
- A term must not appear in both lists simultaneously — consumers fail the
  build if it does.
