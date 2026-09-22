# Upstream Relationship

## Upstream project

**Repository:** `hydralauncher/hydra`

This private repository is an independent research/development workspace based on the upstream Hydra project.

## Provenance

Changes made here should be distinguishable from upstream code.

When importing or synchronizing upstream changes:

- record the upstream commit/tag
- avoid rewriting upstream history unnecessarily
- document local research changes
- review the diff before publication

## Intended Git relationship

The local repository should eventually use:

```text
origin  → https://github.com/rudra-khandelwal/hydra.git
upstream → https://github.com/hydralauncher/hydra.git
```

This allows local work to be pushed to the private repository while upstream changes can be fetched separately.
