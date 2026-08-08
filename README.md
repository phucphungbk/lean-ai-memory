# 🧠 Lean Git-Based AI Memory (Bộ Nhớ AI Tinh Gọn Dựa Trên Git)

A dead-simple, zero-cost, and single-agent framework to manage AI memory for development teams and solo developers. No heavy databases, no cloud APIs, and **strictly NO multi-agent drama**.

Một giải pháp quản lý ký ức cho AI agent cực kỳ đơn giản, chi phí bằng 0 và dành cho mô hình Đơn Đặc Vụ (Single-Agent). Không database cồng kềnh, không API đám mây, và **tuyệt đối KHÔNG có drama giữa các AI agent**.

---

## 🚫 The Problem: Multi-Agent Bloat & Drama
Popular frameworks achieve 100k+ stars by overcomplicating things. They spawn 10 different subagents (Coder, Reviewer, Planner) for a single task.

Just like in a real human office, **"too many cooks spoil the broth"**:
- **The Infinite Loop Conflict:** Agents argue back and forth, burning thousands of tokens.
- **Diffusion of Responsibility:** Agents start blaming each other.
- **Financial Nightmare:** Passing massive contexts spikes your API bills exponentially.

---

## 💡 The Solution: Trust Native Intelligence (1 Chief Engineer + Markdown)
With modern LLMs (Claude 3.5 Sonnet, GPT-4o, DeepSeek), AI is smart enough to understand natural language rules natively. 

This project provides two strict, conflict-free memory protocols:

### 1️⃣ Team Edition (Git-Username Based)
Every developer owns their own memory file (e.g., `history_alex.md`).
- **Zero Git Conflicts:** No binary collisions during `git merge`.
- **Smart Chronological Lookback:** AI scans back (T-1, T-2) through the logs to pick up where you left off.

### 2️⃣ Personal Edition (Daily YYYY-MM-DD Based)
Perfect for solo creators. Memory is bucketed by day (e.g., `2026-08-06.md`).
- **Daily Lookback Protocol:** AI checks today's file first. If empty, it steps back chronologically to find the latest active context.
- **Natural Context Chunking:** Prevents token overflow by keeping daily logs lean and isolated.

---

## 🛠 How to Setup in 1 Minute

1. Create a folder named `.ai-memory` in your project root.
2. Choose your edition from the `templates/` folder in this repository:
   - For Teams: Copy `templates/team-edition.ai.rules` to your project root as `.ai.rules`.
   - For Solo: Copy `templates/personal-edition.ai.rules` to your project root as `.ai.rules`.
3. Done! Tell your AI to read `.ai.rules` before starting any work.

## 🤝 Contributing
Since this framework relies 100% on Natural Language, feel free to open a PR to optimize the prompt rules for newer AI models!