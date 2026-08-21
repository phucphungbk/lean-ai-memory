# Lean AI Memory Specification

**Version:** 0.1

Lean AI Memory is a minimal, human-auditable protocol for maintaining durable project memory for AI agents.

It uses human-readable files, natural-language rules, and Git history instead of requiring a dedicated memory database or vector store.

---

## 1. Goals

Lean AI Memory is designed to provide:

* Persistent memory across AI sessions
* Human-readable and editable memory
* Git-based history and provenance
* Minimal infrastructure
* Project-local memory
* Compatibility with different AI agents and LLMs

Lean AI Memory does **not** attempt to define a universal memory database, retrieval engine, or vector-search system.

---

## 2. Core Principles

### 2.1 Human-readable

Memory SHOULD be stored in plain-text formats, preferably Markdown.

A human should be able to open the repository and understand the stored memory without requiring a specialized application.

### 2.2 Project-local

Memory SHOULD belong to the project that produced it.

The repository itself provides the natural boundary for project memory.

### 2.3 Durable knowledge over conversation history

Agents SHOULD NOT store entire conversations as memory.

Instead, they SHOULD extract information that is expected to remain useful across future sessions.

Examples include:

* Architectural decisions
* Important constraints
* Investigations and their conclusions
* Known problems
* Rejected approaches
* Project-specific conventions

### 2.4 Git as history and provenance

Memory changes SHOULD be versioned together with the project whenever possible.

Git provides:

* History
* Diff
* Review
* Rollback
* Attribution
* Provenance

A memory update SHOULD therefore be understandable as a normal project change.

### 2.5 Human control

Humans SHOULD be able to:

* Read memory
* Edit memory
* Delete memory
* Review memory changes
* Revert incorrect memory

An AI agent MUST NOT be treated as the sole authority over the project's long-term memory.

---

## 3. Memory Rules

A project MAY provide an `.ai.rules` file containing natural-language instructions for memory behavior.

Rules MAY define:

* What information should be remembered
* What information should not be remembered
* Which files should be read
* When memory should be updated
* How memory should be organized
* How obsolete information should be handled

Example:

```text
Before starting work, read relevant project memory.

Only record information that is likely to remain useful
across future sessions.

Do not store raw conversations.

When a previous decision is changed, update the memory
and preserve the reason for the change.

Keep memory concise and project-specific.
```

The protocol does not require a specific rule language.

---

## 4. Memory Lifecycle

A compliant implementation SHOULD follow this general lifecycle:

```text
Read
  ↓
Work
  ↓
Discover
  ↓
Decide
  ↓
Record
  ↓
Review
  ↓
Commit
```

### 4.1 Read

Before starting a task, the agent SHOULD inspect relevant existing memory.

The agent SHOULD avoid loading unrelated memory when it is not needed.

### 4.2 Work

The agent performs the requested task using the available project context and relevant memory.

### 4.3 Discover

During the task, the agent may discover information that could remain useful beyond the current session.

### 4.4 Decide

The agent determines whether the information is durable enough to become memory.

Not every observation should be persisted.

### 4.5 Record

Durable information SHOULD be written to the project's memory files.

### 4.6 Review

Memory changes SHOULD be reviewable through normal project tooling, preferably Git diff.

### 4.7 Commit

Memory MAY be committed together with the corresponding project change.

---

## 5. What Should Become Memory?

Information SHOULD be considered for memory when it has future value.

Examples:

### Decisions

```text
PostgreSQL was selected because transactional consistency
is required by the billing workflow.
```

### Investigations

```text
The authentication failure was caused by expired JWT
tokens not being validated by the middleware.
```

### Constraints

```text
The application must remain compatible with .NET Framework 4.8.
```

### Rejected approaches

```text
Redis was considered but rejected because the deployment
must remain fully local.
```

### Known issues

```text
The CSV importer currently fails when fields contain
embedded line breaks.
```

---

## 6. What Should NOT Become Memory?

Agents SHOULD avoid storing:

* Raw conversations
* Temporary thoughts
* Repeated information
* Intermediate reasoning that has no future value
* Large generated outputs
* Temporary debugging output
* Information that can easily be regenerated
* Secrets or credentials

The goal is not to maximize the amount of stored information.

The goal is to maximize the usefulness of retained information.

---

## 7. Memory Structure

Lean AI Memory does **not** require a fixed directory structure.

A project MAY organize memory according to its own needs.

For example:

```text
.ai-memory/
├── decisions/
├── investigations/
├── known-issues/
└── current.md
```

Another project may use:

```text
.ai-memory/
├── architecture.md
├── decisions.md
└── known-issues.md
```

Both structures are valid.

The protocol defines **memory behavior**, not a mandatory filesystem layout.

---

## 8. Memory Updates

When existing knowledge becomes incorrect, obsolete, or incomplete, the agent SHOULD update the existing memory rather than blindly appending another conflicting statement.

For example:

```text
Previous:
Use Redis for session storage.

Updated:
Redis was evaluated but rejected.
Session state is now stored in PostgreSQL.
Reason: deployment simplicity.
```

The Git history SHOULD preserve the evolution of the decision.

---

## 9. Provenance

Where practical, important memory SHOULD contain enough context to explain where it came from.

For example:

```markdown
## Decision

Use PostgreSQL for session storage.

## Reason

The deployment must remain self-contained.

## Provenance

- Decision made during authentication redesign
- Commit: abc1234
```

Provenance does not require a special database.

Git history MAY provide the primary provenance mechanism.

---

## 10. Context vs Memory

Lean AI Memory distinguishes between **context** and **memory**.

### Context

Information required to perform the current task.

### Memory

Information expected to remain useful after the current task or session.

Therefore:

```text
Current Context
      ↓
Useful discovery
      ↓
Durable knowledge
      ↓
Project Memory
```

An agent SHOULD NOT automatically convert all context into memory.

---

## 11. Retrieval

Lean AI Memory does not mandate a specific retrieval mechanism.

An implementation MAY use:

* File search
* Keyword search
* Git
* Agent-native search
* Semantic search
* Vector databases
* Other indexing mechanisms

However, the underlying memory SHOULD remain understandable without the retrieval layer.

Retrieval is an implementation detail.

Memory is the durable knowledge.

---

## 12. Compatibility

The protocol is LLM-agnostic.

It MAY be implemented by:

* Coding agents
* CLI agents
* IDE assistants
* Autonomous agents
* Custom LLM applications

No specific model is required.

An implementation SHOULD treat the memory files and rules as the source of project-level durable knowledge.

---

## 13. Minimal Compliance

An implementation can be considered a minimal Lean AI Memory implementation if it provides:

1. Human-readable persistent memory
2. Project-local memory
3. Natural-language memory rules
4. Cross-session continuity
5. Human-editable memory
6. Versioned or reviewable memory changes
7. No mandatory memory database

Everything beyond these requirements is optional.

---

## 14. Example

A coding agent starts a new session.

### Session 1

```text
Agent
  ↓
Reads .ai.rules
  ↓
Reads relevant memory
  ↓
Investigates authentication bug
  ↓
Finds root cause
  ↓
Records durable finding
  ↓
Git diff reviewed
  ↓
Commit
```

Memory:

```markdown
# Authentication Investigation

## Finding

JWT expiration was not validated by the authentication middleware.

## Decision

Expiration validation will be performed in middleware
rather than individual controllers.

## Status

Implemented.

## Provenance

Commit: abc1234
```

### Session 2

The agent starts a new session.

```text
Agent
  ↓
Reads rules
  ↓
Reads authentication memory
  ↓
Sees previous investigation
  ↓
Continues from the previous state
```

The agent does not need the entire previous conversation.

It only needs the durable knowledge that survived the session.

---

## 15. Non-Goals

Lean AI Memory is not intended to be:

* A replacement for vector databases
* A universal semantic search engine
* A distributed memory service
* A multi-tenant memory platform
* A conversation archive
* A proprietary LLM memory implementation

Projects requiring these capabilities may use Lean AI Memory alongside other systems.

---

## 16. Philosophy

The protocol follows a simple principle:

> **Store what should survive the session, not everything that happened during the session.**

Memory should remain:

* Small
* Useful
* Inspectable
* Editable
* Versioned
* Reversible

The simplest memory system is often the one that requires the least infrastructure to understand and maintain.
