# Personal Edition

This example demonstrates a personal implementation of Lean AI Memory using chronological daily memory files.

## Memory Strategy

The agent stores project memory under:

```text
.ai-memory/
└── YYYY-MM-DD.md
```

Before starting work, the agent checks today's memory first. If today's file does not exist, it looks backward chronologically to find the latest available memory.

After completing a task, the agent appends durable project knowledge to the current day's memory file.

## Example

```text
.ai.rules
.ai-memory/
└── 2026-08-22.md
```

The `.ai.rules` file defines the complete memory and workflow behavior for this implementation.

The memory structure shown here is an implementation choice and is not required by the Lean AI Memory specification.

See [`SPEC.md`](../../SPEC.md) for the protocol definition.
