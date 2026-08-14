# 🧠 Lean AI Memory

> **"Human-readable memory for AI agents. Markdown + Git + user-defined rules."**

Lean AI Memory is a tiny, Git-native protocol for giving AI agents persistent memory using **Markdown and natural-language rules**.

No database.
No vector store.
No embeddings.
No cloud service.
No complicated infrastructure.

Just:

**Markdown + Git + Rules.**

The goal is simple:

> Let AI remember what matters, while keeping that memory understandable and controllable by humans.

---

## Why?

AI agents are becoming very good at working on long-running projects.

But there is still a simple problem:

**"The AI forgets."**

You may spend hours discussing:

- why an architectural decision was made
- which technology was chosen
- what has already been implemented
- what is still unfinished
- which problem was investigated
- what assumptions were made
- what should happen next

Then the session ends.

Tomorrow, a new AI session starts.

And you have to explain everything again.

There are many possible ways to solve AI memory:

- databases
- vector databases
- embeddings
- RAG
- memory services
- cloud APIs
- knowledge graphs

Those approaches can be useful.

But Lean AI Memory starts with a different question:

> **"What if AI memory was something both AI and humans could simply read, edit, review and version?"**

That is why Lean AI Memory uses Markdown.

---

# 💡 The Core Idea

Lean AI Memory does not try to build another complicated memory engine.

Instead, it gives AI agents a simple shared memory space inside the project.

    AI Agent
       |
-------▼-------
|  .ai.rules  |
|             |
| How AI should |
| use memory  |
---------------
       |
-------▼-------
| .ai-memory/ |
|             |
| Human-readable|
| Markdown memory|
---------------
       |
       ▼
      Git

The AI reads the rules.
The AI reads the relevant memory.
The AI does its work.
The AI records important context.
The next session can continue from that context.
And a human can open the same files at any time.

## 🧠 The Philosophy

Lean AI Memory is intentionally small.
The important idea is not the storage format.
The important idea is **shared understanding**.
AI can read Markdown.
Humans can read Markdown.
Humans can edit Markdown.
Git can version Markdown.
That creates a very simple relationship:

1  AI ⇆ Human-readable memory ⇆ Git

No special memory viewer is required.
No proprietary memory format is required.
No separate memory server is required.
The memory belongs to the project.
And most importantly:

**You can see what the AI remembers.**

## 📜 Rules Are Part of the Memory Model

Memory is only half of the problem.
The other half is:

**What should the AI remember, and when should it remember it?**

Lean AI Memory intentionally does not try to answer this question for everyone.
Instead, the behavior is defined by natural-language rules.
Example:

# AI Memory Rules
Before starting work:
- Read the latest relevant memory. - Check unfinished work. - Check important architecture decisions.
When making an important decision:
- Record the decision. - Record why it was made. - Record important alternatives that were rejected.
When finishing a work session:
- Record completed work. - Record unresolved problems. - Record what should happen next.
Keep memory concise.
Do not store the entire conversation.

These rules are not hard-coded into a memory database.
**You can change them.**

## 🌱 The Rules Are Intentionally Open

Different people need different kinds of memory.
A software developer may want:

Architecture decisions | API changes | Known bugs | Unfinished work | Testing decisions

A documentation project may want:

Terminology | Writing conventions | Audience | Document decisions | Pending sections

A research project may want:

Hypotheses | Evidence | Sources | Rejected assumptions | Open questions

A team may want:

Shared decisions | Project conventions | Responsibilities | Pending work

A personal AI may want something completely different.
Lean AI Memory does not try to define all of these rules.
Instead:

**The memory format is simple. The rules are yours.**

This is intentional.

## ✨ Why Markdown?

Because the simplest format is often the easiest one to understand.
Memory files are ordinary Markdown:

.ai-memory/ ├── 2026-08-14.md ├── 2026-08-15.md └── 2026-08-16.md

You can:

- open them in any editor
- read them without a special tool
- edit them manually
- search them
- review changes
- copy them
- delete them
- restore them
- version them with Git

There is no hidden memory database.
There is no opaque embedding layer.
There is no special viewer required to understand what happened.

## ♾️ Why Git?

Software projects already have a memory system:
**Git.**

Git already provides:

- history
- diff
- branches
- merge
- rollback
- collaboration
- local storage
- remote backup

So why build another system just to version AI memory?
With Markdown files:

git diff

can show exactly what changed in the AI's memory.
You can see:

+ Decided to use PostgreSQL for the new service. 
+ Rejected MongoDB because transactional consistency is required.

The memory becomes part of the project history.

## 🚀 Quick Start

**1. Add `.ai-memory`**

Create a memory directory in your project:

your-project/ ├── .ai-memory/ ├── src/ ├── tests/ └── ...

**2. Add `.ai.rules`**

Choose a template from:

templates/ ├── personal-edition.ai.rules └── team-edition.ai.rules

Copy the appropriate template to your project root:

.ai.rules

**3. Tell your AI agent to follow the rules**

Your AI agent should:

1. Read `.ai.rules`.
2. Read relevant recent memory.
3. Use the existing project context.
4. Record important decisions.
5. Record unfinished work.
6. Keep memory concise.
7. Continue from previous context when possible.

That's it.
There is no server to start.
There is no database to configure.
There is no API key.

## 👤 Personal Edition

For a solo developer, memory can be organized by date:

.ai-memory/ ├── 2026-08-14.md ├── 2026-08-15.md └── 2026-08-16.md

Example:

# 2026-08-14
## Completed
- Added PDF signature verification. - Added Excel export.
## Decisions
- PDF processing remains local. - SQLite is used for local configuration.
## Problems
- Batch verification is still slow.
## Next
- Investigate batch verification. - Improve error reporting.

The next AI session can read this memory and continue from where the previous session stopped.

## 👥 Team Edition

Teams can also keep shared or individual memory.
For example:

.ai-memory/ ├── shared.md ├── history-alice.md ├── history-bob.md └── history-charlie.md

Because everything is plain text, the team can review memory using normal Git tools.

git diff

No special memory infrastructure is required.

## 🔄 A Typical AI Session

**Day 1**
You and your AI agent work on a feature.
During the session:

Decision: Use PostgreSQL instead of MongoDB.
Reason: The feature requires transactional consistency.

The AI records the important context.

.ai-memory/2026-08-14.md

**Day 2**
A new AI session starts.
Instead of asking:

> "Why did we choose PostgreSQL?"

the AI reads the project memory.
It already knows:

PostgreSQL was selected because transactional consistency is required.

The work can continue.

## 🎯 What Lean AI Memory Tries to Solve

Lean AI Memory is useful when you want an AI agent to remember:

*   architectural decisions
*   project conventions
*   previous investigations
*   unfinished work
*   important discoveries
*   assumptions
*   decisions and their reasons
*   what should happen next

It is especially useful for projects that span many AI sessions.

## 🧩 What Makes It Different?

Lean AI Memory deliberately chooses:

| Instead of | Use |
| :--- | :--- |
| Memory database | Markdown |
| Vector store | Plain text |
| Embeddings | Natural-language memory |
| Cloud memory service | Local repository |
| Hidden state | Files humans can inspect |
| Proprietary history | Git history |
| Fixed memory behavior | User-defined rules |

This is not because databases or vector search are bad.
They are useful for different problems.
Lean AI Memory simply asks:

> **Do we really need them for basic project memory?**

Sometimes the answer may be no.

## 🔒 Local First

Lean AI Memory does not require a cloud service.
Your memory can stay inside your project repository.
This means:

*   no memory API
*   no external memory service
*   no vendor lock-in
*   no additional infrastructure

You decide where the repository is stored.

## 🧹 Keep Memory Small

Lean AI Memory is not intended to store every conversation.
Do not turn memory into a transcript.
Instead, store information that is useful for future work.
Good memory:

Decision: Use iText for PDF processing.
Reason: The project already depends on it and replacing it would create unnecessary compatibility issues.

Bad memory:

User: Can you implement this?
AI: Sure, I will start...
User: What about...
AI: Let me think...

The goal is not to remember everything.
The goal is to remember **what matters**.

## 🤖 AI-Agnostic

Lean AI Memory is not tied to a specific AI provider.
The protocol is based on:

*   Markdown
*   Git
*   natural-language rules

It can therefore be adapted to different AI coding assistants and agent workflows.
The project does not need to know which model you use.

## 🌿 What Lean AI Memory Is NOT

This project is intentionally small.
It is not trying to be:

*   a vector database
*   a semantic search engine
*   a knowledge graph
*   an enterprise memory platform
*   a replacement for every AI memory system
*   a universal memory solution for every industry

If you need sophisticated semantic retrieval across millions of memories, this is probably not the right tool.
If you want:

> **"I want my AI to remember this project without adding another service."**

That's what Lean AI Memory is for.

## 🌍 Beyond Coding

Although the initial use case is AI coding agents, the idea is intentionally broader.
The same model can potentially be used for:

Coding | Documentation | Research | Business workflows | Personal AI | Team knowledge | Project management

The important part is not the industry.
The important part is that:

Human ⇆ Readable memory ⇆ AI

can share the same context.
The rules can evolve with the project.

## 📐 Design Principles

**1. Human-readable**
If a human cannot understand the memory, the memory is too opaque.

**2. AI-readable**
The format should be simple enough for AI agents to consume directly.

**3. Local-first**
Memory should live close to the project whenever possible.

**4. Git-native**
Memory should benefit from the same history, diff, branching and collaboration mechanisms as the project.

**5. Rule-driven**
The user defines how memory should be created and maintained.

**6. Keep it small**
Memory should contain useful context, not entire conversations.

**7. AI-agnostic**
Do not lock the memory format to one model or vendor.

**8. Human control**
The user should be able to inspect, edit, remove or restore AI memory at any time.

## 📁 Repository Structure

lean-ai-memory/├── .ai-memory/├── templates/│   ├── personal-edition.ai.rules│   └─ team-edition.ai.rules

The project is intentionally small.
That's part of the design.

## 🤝 Contributing

The core protocol is intentionally simple.
Contributions are welcome, especially:

*   new rule examples
*   better templates
*   real-world usage patterns
*   compatibility improvements
*   documentation
*   ideas for different workflows
*   feedback from using Lean AI Memory in real projects

One thing is especially welcome:

> **Show us how you define your own memory rules.**

We do not want to define every possible rule ourselves.
The interesting part of this project is discovering what people actually need.

## 🗺️ Roadmap

The project intentionally avoids a feature-heavy roadmap.
Possible future directions may include:

*   more rule templates
*   examples for different AI agents
*   team workflows
*   better memory conventions
*   tooling around memory validation
*   optional integrations

Any future feature should preserve the core principles:
**Simple.**
**Human-readable.**
**Git-native.**
**AI-agnostic.**

## Philosophy

> **Maybe AI memory doesn't need to be smarter.**
> **Maybe it just needs to be understandable.**

Lean AI Memory is not an attempt to build the world's most powerful memory engine.
It is an experiment around a simple idea:

> **AI and humans should be able to share a memory that both can understand.**

The storage format is deliberately boring.
The rules are deliberately open.
The infrastructure is deliberately minimal.
Because perhaps the interesting part is not building a bigger memory system.
Perhaps the interesting part is deciding:

> **What should AI remember?**

And that is something we may not want one tool to decide for everyone.