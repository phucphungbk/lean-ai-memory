# 🧠 Lean AI Memory

> **Your AI memory should be a Git diff, not a database.**

A tiny, zero-cost memory protocol for AI coding agents.

**Markdown + Git. That's it.**

No vector database.
No embeddings.
No cloud API.
No extra service.
No complicated infrastructure.

Lean AI Memory gives your AI coding agent a simple way to **remember what happened in your project and continue where it left off.**

---

## Why?

AI coding agents are powerful, but long-running projects have a simple problem:

**The AI forgets.**

You may spend hours discussing:

* Why a design decision was made
* Which database was chosen
* What has already been implemented
* What is still unfinished
* Which bug was investigated
* What should happen next

Then you start a new session.

And the context is gone.

Lean AI Memory stores the important context as ordinary Markdown files inside your Git repository.

So your project history becomes part of the project itself.

---

## 💡 The Idea

Instead of building another memory service:

```text
AI Agent
   │
   ├── Read project rules
   │
   ├── Read recent memory
   │
   ├── Work on the project
   │
   └── Write important decisions
          │
          ▼
      Markdown
          │
          ▼
         Git
```

Your memory is:

* Human-readable
* Version-controlled
* Diffable
* Searchable
* Portable
* Easy to delete
* Easy to restore

And most importantly:

**You own it.**

---

## ✨ What Makes It Lean?

| Traditional AI Memory | Lean AI Memory   |
| --------------------- | ---------------- |
| Database              | Markdown         |
| Vector store          | Git              |
| Embeddings            | Plain text       |
| Cloud service         | Local repository |
| API cost              | $0               |
| Extra infrastructure  | None             |
| Hard to inspect       | `git diff`       |
| Hard to restore       | `git checkout`   |

This project intentionally chooses **simplicity over infrastructure**.

---

# 🚀 Quick Start

## 1. Create the memory directory

In your project:

```text
your-project/
├── .ai-memory/
├── src/
├── tests/
└── ...
```

## 2. Copy a template

Choose one of the templates:

```text
templates/
├── personal-edition.ai.rules
└── team-edition.ai.rules
```

Copy the template you want to your project root:

```text
.ai.rules
```

## 3. Tell your AI agent to follow `.ai.rules`

The rules tell the agent:

1. Read recent memory before starting work.
2. Use the existing project context.
3. Record important decisions.
4. Record unfinished work.
5. Keep memory concise.
6. Continue from the previous context when possible.

That's it.

---

# 👤 Personal Edition

For a solo developer, memory can be organized by date:

```text
.ai-memory/
├── 2026-08-10.md
├── 2026-08-11.md
└── 2026-08-12.md
```

A new session can look at the most recent memory and continue from there.

Example:

```markdown
# 2026-08-12

## Completed
- Added PDF signature verification.
- Exported verification results to Excel.

## Decisions
- SQLite is used for local license storage.
- PDF processing remains completely local.

## Next
- Add batch verification.
- Improve error reporting.
```

Tomorrow, the AI can start from this context instead of starting from zero.

---

# 👥 Team Edition

For teams, each developer can maintain their own memory:

```text
.ai-memory/
├── history_alice.md
├── history_bob.md
└── history_charlie.md
```

This keeps personal working context separate while remaining inside the same Git repository.

Because the files are plain text, developers can review changes with normal Git tools.

```bash
git diff
```

No special memory database is required.

---

# 🔍 Why Markdown + Git?

Because software projects already have a memory system:

**Git.**

Git already gives us:

* History
* Diff
* Branches
* Merge
* Rollback
* Collaboration
* Local storage
* Remote backup

Why build another system when the project already has one?

Lean AI Memory simply gives the AI a structured way to use it.

---

# 🎯 Design Principles

### 1. Local-first

Your memory lives with your project.

### 2. Human-readable

Open the file.

Read it.

Edit it.

No special viewer required.

### 3. Git-native

Memory changes are ordinary Git changes.

### 4. Zero infrastructure

No database server.

No vector database.

No API key.

No cloud dependency.

### 5. Keep memory small

Memory is not a transcript of every conversation.

Only keep information that helps the next session.

### 6. AI-agnostic

The protocol is based on plain Markdown and natural-language rules.

It can be adapted to different AI coding assistants.

---

# 🧪 What Lean AI Memory Is NOT

This project is intentionally small.

It is **not** trying to be:

* A vector database
* A semantic search engine
* A knowledge graph
* An enterprise memory platform
* A replacement for every AI memory system

If you need sophisticated retrieval across millions of memories, this is probably not the right tool.

If you want:

> **"I want my coding AI to remember this project without adding another service."**

That's exactly what this project is for.

---

# 📁 Repository Structure

```text
lean-ai-memory/
│
├── .ai-memory/
│
├── templates/
│   ├── personal-edition.ai.rules
│   └── team-edition.ai.rules
│
├── .gitignore
├── LICENSE
└── README.md
```

---

# 🤝 Contributing

The core of Lean AI Memory is intentionally simple.

Contributions are welcome, especially:

* Better memory rules
* Better examples
* Compatibility improvements
* New usage patterns
* Real-world feedback

If you use Lean AI Memory in a real project, I'd love to hear what worked and what didn't.

---

# ⭐ Philosophy

> **Keep the intelligence in the AI.
> Keep the memory in Git.**

The goal isn't to build a bigger memory system.

The goal is to make AI coding agents **remember enough to be useful, without adding unnecessary infrastructure.**

---

## License

MIT
