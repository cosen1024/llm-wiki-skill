# LLM Wiki Skill

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

Build and maintain a persistent, compounding knowledge base using the **Karpathy Wiki** pattern. This is a skill designed for **Claude Code** and **Accio** users who want their AI to actually "learn" and "remember" across sessions.

---

## 🚀 Why this?

**This is NOT RAG.** 
Standard RAG (Retrieval-Augmented Generation) re-derives knowledge from raw documents every time you ask a question. It has no memory and no accumulation. 

**LLM Wiki compiles knowledge.**
Like a programmer compiling source code into a binary, the LLM reads your raw materials once and "compiles" them into a structured, interlinked Markdown Wiki. 
- **Accumulation**: Every source added makes the wiki richer.
- **Context**: The LLM understands the *connections* between different sources.
- **Persistence**: Knowledge lives in your local files, not in a hidden vector database.

> "Obsidian is the IDE. The LLM is the programmer. The wiki is the codebase."

## 📂 Architecture

```text
vault/
├── raw/              # IMMUTABLE. Raw PDFs, articles, notes. LLM reads only.
├── wiki/             # LLM-OWNED. The compiled knowledge.
│   ├── CLAUDE.md         # ★ The Schema: Domain-specific rules and workflows.
│   ├── index.md          # Navigation map for the LLM.
│   ├── log.md            # Append-only operation history.
│   ├── overview.md       # High-level synthesis of everything.
│   ├── sources/          # Summaries linked back to raw files.
│   ├── concepts/         # Deep dives into specific topics.
│   └── entities/         # People, tools, and organizations.
└── output/           # Valuable results (reports, slides) that flow back to Wiki.
```

## 🛠️ Operations

| Command | Action |
|---|---|
| `build wiki` | Initialize the structure and co-evolve the `CLAUDE.md` schema. |
| `ingest this` | Process a raw source and weave it into the wiki fabric. |
| `wiki query` | Ask questions and generate "flowback" artifacts. |
| `lint wiki` | Perform a health check: find gaps, contradictions, and orphans. |

## 📦 Installation

Since this is a skill for Claude Code/Accio:

1. Clone this repository to your skills directory:
   ```bash
   git clone https://github.com/your-username/llm-wiki-skill.git
   ```
2. In your AI agent, point to the `SKILL.md` file.

## 🌟 Best Practices

- **Flowback is magic**: Always file valuable query results back into the wiki.
- **Just dump into raw/**: Don't worry about organization; let the LLM handle the structure.
- **Use Obsidian**: Use it as your viewer. The LLM writes, you browse.

## 🤝 Credits

![Karpathy's Vision](https://images.javalearn.cn/blog/2026/04/eeea3ed3aeb2783bbf055dcfc81d164b.png)

Inspired by [Andrej Karpathy's LLM Wiki concept](https://karpathy.ai/blog/wiki.html).

## 📄 License

MIT
pired by [Andrej Karpathy's LLM Wiki concept](https://karpathy.ai/blog/wiki.html).

## 📄 License

MIT
