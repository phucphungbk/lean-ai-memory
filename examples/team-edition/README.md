# Team Edition

This example demonstrates a team implementation of Lean AI Memory using developer-specific memory histories.

## Memory Strategy

The agent identifies the current developer's Git username and uses a corresponding memory file:

```text
.ai-memory/
├── history_<username>.md
```

Before modifying code, the agent reads the developer's existing history.

After completing a task, the agent appends durable project knowledge to the same history file.

## Example

```text
.ai.rules
.ai-memory/
├── history_developer1.md
└── history_developer2.md
```

Each developer maintains an independent history while sharing the same project repository.

The `.ai.rules` file defines the complete memory and workflow behavior for this implementation.

The memory structure shown here is an implementation choice and is not required by the Lean AI Memory specification.

See [`SPEC.md`](../../SPEC.md) for the protocol definition.
