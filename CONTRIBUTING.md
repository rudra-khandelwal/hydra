# Contributing

This is a personal public research/development workspace.

## Change discipline

Prefer small, traceable changes.

Before committing:

1. Read `docs/PROJECT-MEMORY.md`.
2. Inspect the current target files.
3. Search for duplicate or legacy implementations.
4. Remove secrets and unnecessary personal data.
5. Run the relevant build/syntax/test command.
6. Review the actual diff/result.
7. Update validation/memory/diary records when the project state changes.
8. For Pages changes, inspect workflow annotations as well as the final conclusion.

## Research entries

Use:

**Fact → Observation → Hypothesis → Finding → Next Action**

Clearly label whether a statement is an observation, an inference, or a verified finding.

## Live-guide status

Use these terms precisely:

- **Implemented** — present in repository source.
- **Deployed** — Pages deployment succeeded for the relevant commit.
- **Live-verified** — the published behavior was actually exercised.

Do not call source inspection alone “live verification”.

## Attribution

When preserving AI-assisted work, identify the source as [CHATGPT] or [CLAUDE] where the distinction matters.

## Commit messages

Prefer:

- `docs: ...`
- `research: ...`
- `security: ...`
- `build: ...`
- `fix: ...`
- `chore: ...`
