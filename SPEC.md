# Lean AI Memory Specification

**Version:** 0.1

Lean AI Memory is a minimal, human-auditable protocol for maintaining durable project memory across AI sessions.

It uses human-readable files, project-defined rules, and version control to preserve useful knowledge without requiring a dedicated memory database or vector store.

---

## 1. Goals

Lean AI Memory is designed to provide:

* Persistent memory across AI sessions
* Human-readable and editable memory
* Project-local context
* Git-based history and provenance
* Minimal infrastructure
* Flexible memory organization
* Compatibility with different AI agents and LLMs

Lean AI Memory defines **principles and behavior**, not a mandatory filesystem schema.

---

## 2. Core Principles

### 2.1 Human-readable

Memory SHOULD be stored in human-readable formats, preferably plain text or Markdown.

A human should be able to inspect, edit, review, and remove memory without requiring a specialized memory service.

### 2.2 Project-local

Memory SHOULD belong to the project or workspace that produced it.

The project repository SHOULD provide the natural boundary for project memory.

### 2.3 Durable knowledge over conversation history

Agents SHOULD store information that is expected to remain useful beyond the current session.

Agents SHOULD NOT treat the entire conversation as memory.

Examples of durable knowledge include:

* Important decisions
* Project constraints
* Discovered behavior
* Root causes
* Known issues
* Rejected approaches
* Project-specific conventions

### 2.4 Human control

Humans SHOULD be able to:

* Read memory
* Edit memory
* Delete memory
* Review memory changes
* Revert incorrect memory

AI agents SHOULD NOT be treated as the sole authority over long-term project memory.

### 2.5 Versioned history

Memory changes SHOULD be reviewable through version control when the project uses version control.

Git is the preferred mechanism when the project is hosted in Git.

Version control provides:

* History
* Diff
* Rollback
* Review
* Provenance

---

## 3. Rules

A Lean AI Memory implementation SHOULD define rules that tell an AI agent how memory is handled.

Rules MAY define:

* Where memory is stored
* How relevant memory is discovered
* What information should be remembered
* What information should not be remembered
* When memory should be updated
* How memory should be organized
* How obsolete information should be handled
* How multiple developers or agents share memory

Rules SHOULD be expressed in a form that the target AI agent can understand.

Natural-language rules are recommended because they remain human-readable and can be adapted to different agents.

---

## 4. Memory Retrieval

Before performing work, an agent SHOULD retrieve memory relevant to the current task.

The retrieval strategy is implementation-defined.

An implementation MAY use:

* A current memory file
* Chronological lookback
* Developer-specific history
* Project-wide memory
* Keyword search
* File search
* Semantic search
* Vector search
* Agent-native retrieval

Lean AI Memory does not require a specific retrieval algorithm.

The important requirement is that relevant durable project knowledge can be restored across sessions.

---

## 5. Memory Storage

Memory MUST remain accessible as durable project knowledge.

The protocol does **not** require a fixed directory structure or naming convention.

For example, an implementation MAY use chronological files:

```text
.ai-memory/
├── 2026-08-20.md
├── 2026-08-21.md
└── 2026-08-22.md
```

Another implementation MAY use developer-specific histories:

```text
.ai-memory/
├── history_alice.md
├── history_bob.md
└── history_charlie.md
```

Another implementation MAY organize memory by knowledge type:

```text
.ai-memory/
├── decisions.md
├── architecture.md
└── known-issues.md
```

All of these can be valid Lean AI Memory implementations.

The protocol defines **behavior**, not a mandatory memory schema.

---

## 6. Memory Lifecycle

A typical Lean AI Memory workflow is:

```text
Retrieve
   ↓
Work
   ↓
Discover
   ↓
Evaluate
   ↓
Record
   ↓
Review
   ↓
Version
```

### 6.1 Retrieve

Read relevant existing memory before performing work.

### 6.2 Work

Perform the requested task using the available project context.

### 6.3 Discover

Identify information discovered during the task that may remain useful in future sessions.

### 6.4 Evaluate

Determine whether the information is durable enough to become memory.

Not every observation should be persisted.

### 6.5 Record

Store durable information according to the project's memory rules.

### 6.6 Review

Memory changes SHOULD remain understandable to humans.

When using Git, `git diff` SHOULD be sufficient to review normal memory changes.

### 6.7 Version

Memory changes SHOULD be preserved through the project's version-control mechanism when available.

---

## 7. What Should Become Memory?

Information SHOULD be considered for storage when it has meaningful future value.

Examples:

### Decision

```markdown
PostgreSQL was selected for session storage because
the deployment must remain self-contained.
```

### Constraint

```markdown
The application must remain compatible with .NET Framework 4.8.
```

### Investigation

```markdown
The authentication failure was caused by JWT expiration
not being validated by the middleware.
```

### Rejected approach

```markdown
Controller-level JWT validation was rejected because
authentication rules should remain centralized.
```

### Known issue

```markdown
The CSV importer currently fails when fields contain
embedded line breaks.
```

---

## 8. What Should Not Become Memory?

Agents SHOULD avoid storing:

* Raw conversations
* Temporary thoughts
* Repeated information
* Intermediate reasoning with no future value
* Large generated outputs
* Temporary debugging output
* Information that can easily be regenerated
* Secrets or credentials

The objective is not to maximize the amount of stored information.

The objective is to preserve information that remains useful.

---

## 9. Memory Updates

When existing knowledge becomes incorrect, obsolete, or incomplete, an implementation SHOULD update the existing memory according to its rules.

It SHOULD avoid creating contradictory memory entries when the previous information can be updated.

For example:

```markdown
Previous:

Use Redis for session storage.

Updated:

Redis was evaluated but rejected.
Session state is now stored in PostgreSQL.
Reason: deployment simplicity.
```

When version control is used, the history of this change provides additional provenance.

---

## 10. Provenance

Important memory SHOULD contain enough information to understand its origin when practical.

Possible provenance includes:

* Git commit
* Date
* Developer
* Related file
* Related task
* Investigation
* Decision
* Issue

The protocol does not require a dedicated provenance database.

Version control MAY serve as the primary provenance mechanism.

---

## 11. Context vs Memory

Lean AI Memory distinguishes between **context** and **memory**.

### Context

Information required to perform the current task.

### Memory

Information expected to remain useful after the current task or session.

Therefore:

```text
Current Context
      ↓
Useful Discovery
      ↓
Durable Knowledge
      ↓
Project Memory
```

An agent SHOULD NOT automatically convert all context into memory.

Memory is a deliberate subset of context.

---

## 12. Multiple Memory Strategies

Different projects MAY use different memory strategies while remaining compatible with the protocol.

For example:

### Personal Edition

A personal workflow may maintain chronological daily memory:

```text
.ai-memory/
├── 2026-08-20.md
├── 2026-08-21.md
└── 2026-08-22.md
```

The agent retrieves the latest relevant history and appends new information to the current day's memory.

### Team Edition

A team workflow may maintain developer-specific history:

```text
.ai-memory/
├── history_alice.md
├── history_bob.md
└── history_charlie.md
```

The agent identifies the current developer and retrieves the corresponding history before performing work.

These are **implementation strategies**, not protocol requirements.

The same Lean AI Memory principles apply to both.

---

## 13. Retrieval and Storage Are Independent

A project may change how memory is retrieved without changing how memory is stored.

For example:

```text
Markdown Memory
      ↓
Keyword Search
```

may later become:

```text
Markdown Memory
      ↓
Semantic Index
      ↓
Relevant Memory
```

The underlying human-readable memory remains the durable source.

Retrieval is an implementation detail.

---

## 14. LLM and Agent Compatibility

Lean AI Memory is LLM-agnostic.

It MAY be used with:

* Coding agents
* CLI agents
* IDE assistants
* Autonomous agents
* Custom LLM applications

No specific model, vendor, API, or agent framework is required.

An implementation SHOULD adapt the rules to the capabilities of its target agent.

---

## 15. Minimal Compliance

A minimal Lean AI Memory implementation SHOULD provide:

1. Persistent project memory
2. Human-readable memory
3. Rules describing memory behavior
4. Cross-session retrieval
5. Human-editable memory
6. Reviewable memory changes
7. A mechanism for preserving memory history

The following are optional:

* Vector databases
* Semantic indexing
* Embeddings
* Memory ranking
* MCP servers
* APIs
* Automated summarization
* External memory services

These technologies MAY improve an implementation but are not part of the core protocol.

---

## 16. Non-Goals

Lean AI Memory is not intended to be:

* A universal memory database
* A mandatory vector database
* A conversation archive
* A distributed memory service
* A multi-tenant memory platform
* A proprietary LLM memory implementation
* A replacement for every existing AI memory system

Projects requiring these capabilities MAY use Lean AI Memory together with additional systems.

---

## 17. Example Workflow

A coding agent starts a new session.

```text
Read project rules
       ↓
Retrieve relevant memory
       ↓
Understand previous project state
       ↓
Perform requested work
       ↓
Discover durable knowledge
       ↓
Record memory according to project rules
       ↓
Review memory changes
       ↓
Commit project changes
```

The next session repeats the process:

```text
New Session
     ↓
Retrieve previous memory
     ↓
Continue from durable knowledge
```

The agent does not need the entire previous conversation.

It only needs the information that was intentionally preserved.

---

## 18. Philosophy

Lean AI Memory follows a simple principle:

> **Store what should survive the session, not everything that happened during the session.**

The protocol favors memory that is:

* Small
* Useful
* Human-readable
* Inspectable
* Editable
* Versioned
* Reversible

The goal is not to build the most sophisticated memory system.

The goal is to make AI memory **simple enough to understand, control, and maintain**.
