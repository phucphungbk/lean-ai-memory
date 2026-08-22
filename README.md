# 🧠 Lean AI Memory

> **What if AI memory didn't need another database?**

Lean AI Memory is a small, Git-native protocol for persistent memory in AI coding agents.

It explores a simple question:

> **Can useful project memory be maintained with plain text, Git, and a small set of agent rules?**

Instead of starting with a memory database, embedding pipeline, or retrieval service, Lean AI Memory starts with the simplest possible building blocks:

**Plain text + Git + AI rules**

This project is intentionally small.

It is not trying to build another memory engine.

It is an experiment and an open protocol for exploring how AI agents can preserve useful project knowledge across sessions.

---

## Why Lean AI Memory?

AI coding agents are becoming increasingly capable, but maintaining useful context across sessions remains difficult.

An agent may understand the current conversation while losing important project knowledge when the session ends.

A typical memory architecture may look like:

```text
AI Agent
   ↓
Embedding
   ↓
Vector Database
   ↓
Retrieval
   ↓
Context
```

Lean AI Memory starts with a simpler baseline:

```text
AI Agent
   ↓
.ai.rules
   ↓
Human-readable memory
   ↓
Git
```

The project already has a filesystem and Git.

So the first question is not:

> "What memory infrastructure should we build?"

It is:

> **"How far can simple project-local memory take us?"**

---

## Core Idea

Lean AI Memory separates **context** from **memory**.

### Context

Information needed to complete the current task.

### Memory

Information expected to remain useful after the current task or session.

```text
Current Context
      ↓
Useful Discovery
      ↓
Durable Knowledge
      ↓
Project Memory
```

An agent should not automatically remember everything.

Instead, it evaluates what is likely to remain useful and preserves only that durable knowledge.

The goal is:

> **Store what should survive the session, not everything that happened during the session.**

---

## 🧩 The Three Building Blocks

### 1. Plain Text

Memory is stored in human-readable files, preferably Markdown.

No proprietary memory database is required.

Humans can:

- Read it
- Edit it
- Delete it
- Review it
- Search it

---

### 2. Git

Git provides history and provenance.

Memory changes can be:

- Diffed
- Reviewed
- Committed
- Reverted
- Traced

```text
Memory
   ↓
Git diff
   ↓
Commit
   ↓
History
```

Memory therefore becomes part of the project's normal development history.

---

### 3. AI Rules

`.ai.rules` defines how an AI agent should interact with memory.

Rules can determine:

- Where memory is stored
- How relevant memory is retrieved
- What should be remembered
- What should not be remembered
- When memory should be updated
- How memory is organized

The rules are intentionally flexible.

Lean AI Memory defines the **protocol**, not a mandatory directory structure.

---

## 🔄 Typical Workflow

A typical session looks like:

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
Continue
```

### Retrieve

The agent reads relevant project memory before beginning work.

### Work

The agent performs the requested task using the existing project context.

### Discover

The agent identifies useful technical knowledge discovered during the task.

### Evaluate

The agent decides whether that knowledge is durable enough to survive the session.

### Record

Durable knowledge is added to project memory according to `.ai.rules`.

### Review

Memory changes remain visible through normal project tooling and Git diff.

### Continue

The next session retrieves the preserved knowledge instead of requiring the entire previous conversation.

---

## 💬 An Open Question

Lean AI Memory does **not** claim that Markdown + Git is the best solution for every AI memory problem.

It asks a narrower question:

> **For project-level memory, how far can we get with simple, human-readable, Git-native storage and agent rules?**

There are many questions worth exploring:

- When does plain-text memory stop scaling?
- How should an agent decide what is worth remembering?
- Should memory be chronological, semantic, or decision-based?
- How should obsolete memories be updated or removed?
- How should multiple developers share durable project knowledge?
- How much retrieval logic is actually necessary?
- When does semantic search become useful?
- Do different AI agents need different memory rules?
- What happens when memory becomes large?
- Can Git history provide enough provenance for AI memory?

These are intentionally open questions.

**Discussion, experiments, benchmarks, and alternative implementations are welcome.**

---

## 👤 Personal Edition

A personal workflow can use chronological daily memory.

Example:

```text
.ai-memory/
├── 2026-08-20.md
├── 2026-08-21.md
└── 2026-08-22.md
```

The agent can:

1. Check today's memory first.
2. If it does not exist, look backward for the latest available memory.
3. Use that memory as context.
4. Append durable knowledge to today's memory.

This is only one possible implementation strategy.

See [`examples/personal-edition`](./examples/personal-edition/) for a complete example.

---

## 👥 Team Edition

A team can use developer-specific memory while sharing the same repository.

Example:

```text
.ai-memory/
├── history_alice.md
├── history_bob.md
└── history_charlie.md
```

The agent identifies the current developer's Git username and uses the corresponding history file.

For example:

```text
.ai-memory/history_alice.md
```

This allows each developer to maintain personal working history while sharing the same project.

Team-specific memory organization is an implementation choice, not a protocol requirement.

See [`examples/team-edition`](./examples/team-edition/) for a complete example.

---

## 📐 Specification

Lean AI Memory defines the principles and behavior of the memory protocol without prescribing a fixed memory schema.

The protocol does **not** require:

- A specific directory structure
- A specific filename convention
- A specific LLM
- A vector database
- An embedding model
- A retrieval engine
- A specific AI coding agent

Read the full specification:

**[SPEC.md](./SPEC.md)**

---

## 🔎 Retrieval

Lean AI Memory does not require a dedicated retrieval engine.

For small and medium project memory, AI agents can use tools that already exist in the development environment.

For example:

### Git

```bash
git grep "authentication" -- .ai-memory/
```

Git history can also be used to understand how memory evolved:

```bash
git log -- .ai-memory/
```

Specific changes can be investigated with:

```bash
git log -S "PostgreSQL" -- .ai-memory/
```

### grep

On Unix-like systems:

```bash
grep -R "authentication" .ai-memory/
```

### PowerShell

On Windows:

```powershell
Get-ChildItem .ai-memory -Recurse -File |
    Select-String "authentication"
```

### IDE Search

Most development environments already provide project-wide text search.

This means the basic retrieval path can remain:

```text
AI Agent
    ↓
Project Search
    ↓
.ai-memory/
```

No additional search service is required for the baseline protocol.

A dedicated indexing or semantic retrieval layer should only be introduced when real usage demonstrates that basic project search is no longer enough.

---

## 🧠 Design Principles

### Minimal

Use existing project infrastructure whenever possible.

### Human-Auditable

Memory should be understandable by humans without specialized tooling.

### Project-Local

Memory belongs to the project and its development history.

### Versioned

Memory changes should be reviewable and reversible.

### Rule-Driven

The project decides what and how the AI should remember.

### Model-Agnostic

Lean AI Memory does not depend on a specific LLM or vendor.

### Durable Over Complete

The objective is not to preserve everything.

The objective is to preserve what remains useful.

---

## 🔍 Start Simple, Then Measure

Vector databases, embeddings, semantic retrieval, and dedicated memory systems can be useful.

Lean AI Memory does not reject them.

The project starts with a simpler baseline:

```text
Markdown + Git + Rules + Existing Project Tools
```

For basic retrieval, existing tools such as `git grep`, `grep`, `Select-String`, IDE search, and Git history may already be sufficient.

The interesting question is what happens when we actually test that baseline.

If a project becomes large enough that plain-text storage or basic retrieval is no longer effective, that is useful information.

An indexing layer, semantic search, or another retrieval mechanism can then be explored without changing the core idea of durable, human-auditable memory.

The goal is not:

> "Never use a vector database."

The goal is:

> **"Don't add memory infrastructure before we know we need it."**

---

## 📁 Repository Structure

```text
lean-ai-memory/
├── .ai-memory/
├── templates/
│   ├── personal-edition.ai.rules
│   └── team-edition.ai.rules
├── examples/
│   ├── personal-edition/
│   │   ├── .ai.rules
│   │   ├── README.md
│   │   └── .ai-memory/
│   └── team-edition/
│       ├── .ai.rules
│       ├── README.md
│       └── .ai-memory/
├── README.md
├── SPEC.md
└── LICENSE
```

The repository intentionally remains small.

The protocol defines memory behavior, while the examples demonstrate different implementation strategies.

---

## 🛣️ Roadmap

### Phase 1 — Core Protocol

- [x] Plain-text memory
- [x] Git-based history
- [x] AI rules
- [x] Personal Edition
- [x] Team Edition
- [x] Protocol specification
- [x] Implementation examples

### Phase 2 — Community Experiments

- [ ] Test with different AI coding agents
- [ ] Test Personal and Team workflows in real projects
- [ ] Collect alternative memory strategies
- [ ] Document real-world usage
- [ ] Explore memory retrieval strategies
- [ ] Explore memory lifecycle and decay
- [ ] Explore memory conflict and correction
- [ ] Explore stale memory detection
- [ ] Compare chronological vs decision-based memory
- [ ] Collect community benchmarks
- [ ] Collect failure cases
- [ ] Community discussion

### Phase 2.5 — Protocol Evolution

- [ ] Identify common patterns across implementations
- [ ] Document interoperability requirements
- [ ] Refine memory lifecycle semantics
- [ ] Define guidance for obsolete memory
- [ ] Define guidance for conflicting memory
- [ ] Update SPEC based on community evidence

### Phase 3 — Optional Tooling

Only if real usage demonstrates a need:

- [ ] Memory validation
- [ ] Memory health checks
- [ ] Stale memory detection
- [ ] Memory conflict detection
- [ ] Memory migration tools
- [ ] Agent integrations
- [ ] Optional indexing for large memory sets

Tooling should remain optional and should not become a requirement of the core protocol.

---

## 🤝 Join the Discussion

Lean AI Memory is intentionally open to criticism and alternative approaches.

You do not need to agree with the design.

If you think:

- Markdown is not enough
- Git is not the right provenance layer
- Memory should be semantic
- Daily memory is a bad strategy
- Team memory needs a different model
- Memory retrieval needs more structure
- The protocol is missing something

Open an Issue or Discussion and show us what you would do differently.

**Alternative implementations are welcome.**

The goal is to discover the simplest memory model that actually works in real AI-assisted development.

---

## 🤝 Contributing

Contributions are welcome.

Ideas, experiments, alternative memory strategies, and real-world usage reports are especially useful.

If you build another implementation strategy, consider contributing it as an example rather than changing the core protocol.

---

## 📄 License

MIT License

---

## Philosophy

> **AI memory doesn't have to be smarter.**
>
> **It has to be understandable, useful, and under human control.**

Lean AI Memory keeps the infrastructure small so the memory itself can remain visible.