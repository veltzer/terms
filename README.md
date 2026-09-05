# shared-terms

Shared technical-terms registry used across the veltzer documentation
projects (`teaching-syllabi`, `teaching-slides`, ...). Like `shared-themes`,
it is consumed as a git submodule mounted at `shared/shared-terms/`.

## Layout

- `unambiguous/` — terms that unambiguously refer to a technology and
  SHOULD be wrapped in backticks in prose
  (e.g. `Python`, `Kubernetes`, `Apache HTTP Server`).
- `ambiguous/` — terms that collide with common English words and MUST NOT
  be wrapped in backticks (e.g. `Apache`, `Spring`, `Go`, `find`, `Agile`).

A term must appear in exactly one of the two registries. Files within each
directory are split by topic for readability — the consumers concatenate
them at load time.

## Consumers

Each consuming project adds this repo as a submodule at
`shared/shared-terms/` and points the `rsconstruct` `terms` checker at it:

```toml
[processor.terms]
dir_terms_unambiguous = "shared/shared-terms/unambiguous"
dir_terms_ambiguous = "shared/shared-terms/ambiguous"
```

The checker reads these to enforce backticking conventions in markdown
source.

## Editing

- Add unambiguous proper-noun product names to `unambiguous/`.
- Add anything that overlaps with English to `ambiguous/`.
- A term must not appear in both lists simultaneously — consumers fail the
  build if it does.
