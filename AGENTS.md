# Repository Working Agreement

This file defines how Codex should collaborate on this project.

## Collaboration Rules

- Plan before coding for any non-trivial task.
- Before editing or creating files, tell the user which files are expected to change.
- Work one Jira ticket at a time unless the user asks to batch work.
- Keep changes focused on the current ticket or decision.
- Do not add dependencies, major tooling, or new architectural patterns without asking first.
- Surface tradeoffs when there is more than one reasonable approach.
- Call out risks, assumptions, or blockers clearly and early.
- After each task, summarize what changed and how to verify it.

## Architecture-First Workflow

Use this default flow unless the user asks for something smaller or faster:

1. Restate the ticket or goal.
2. Identify impacted files and planned changes.
3. Update architecture or reference docs if the decision affects the project shape.
4. Implement the smallest useful slice.
5. Verify behavior.
6. Update project tracking docs if needed.

## Editing Rules

- Prefer small, reviewable changes.
- Preserve existing project patterns once they are established.
- Avoid unrelated cleanup unless the user asks for it.
- If a change affects architecture, data shape, or workflow, update the relevant docs in `docs/`.

## Project Documentation

The following files should be treated as living references:

- `Project_Start.md`: original project prompt and initial scope
- `docs/README.md`: index of the docs folder and when each project doc should be used or updated
- `docs/architecture.md`: current architectural direction
- `docs/ticket-tracker.md`: current, upcoming, and completed work
- `docs/decision-log.md`: important technical decisions and rationale

## Definition of Success Per Task

A task is in good shape when:

- the requested outcome is implemented or the decision is documented
- any important assumptions are stated
- impacted docs are updated when necessary
- the user is told what changed and how to verify it
