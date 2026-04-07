# LLM Wiki Skill

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

[中文版](#-为什么选择它) | [English Version](#-why-this)

---

## 🚀 为什么选择它？

**这不是 RAG。**
传统的 RAG（检索增强生成）在你提问时，临时从文档中抓取信息。它没有记忆，也没有积淀。

**LLM Wiki 是“知识编译”。**
就像程序员将源代码编译成二进制文件一样，LLM 只需读取一次原始资料，并将其“编译”成一个结构化、互联的 Markdown 维基百科。
- **复利效应**：每增加一个来源，维基都会变得更丰富。
- **上下文感知**：LLM 能够理解不同资料之间的“联系”。
- **持久化**：知识存储在你的本地文件中，而不是隐藏的向量数据库中。

> “Obsidian 是 IDE，LLM 是程序员，Wiki 则是代码库。”

## 📂 目录架构

![LLM Wiki 架构图](https://images.javalearn.cn/blog/2026/04/ca4ced3ee79e5d70344731a61d1d7968.png)

```text
vault/
├── raw/              # 不可变层。存放原始 PDF、文章、笔记。LLM 只读。
├── wiki/             # LLM 维护层。编译后的知识产物。
│   ├── CLAUDE.md         # ★ Schema：定义特定领域的规则和工作流。
│   ├── index.md          # 导航地图：供 LLM 快速检索。
│   ├── log.md            # 操作日志：追加记录历史操作。
│   ├── overview.md       # 高层综述：对整个库的系统总结。
│   ├── sources/          # 来源摘要：链接回 raw 原始文件。
│   ├── concepts/         # 概念解析：对特定主题的深度探讨。
│   └── entities/         # 实体：人物、工具、组织。
└── output/           # 结果层：生成的报告、PPT 等，可“回流”至 Wiki。
```

## 🛠️ 核心操作

![LLM Wiki 工作流](https://images.javalearn.cn/blog/2026/04/3a9c6c9b036cd38b527dc4bf9ee87dbc.png)

| 指令 (Trigger) | 功能描述 |
|---|---|
| `build wiki` | 初始化结构，并与 LLM 共同进化 `CLAUDE.md` 规范。 |
| `ingest this` | 摄取原始素材，并将其织入维基百科的织锦中。 |
| `wiki query` | 基于已有的维基知识库提问，并生成可回流的产物。 |
| `lint wiki` | 健康检查：发现知识盲区、矛盾点和孤儿页面。 |

## 📦 安装 (Installation)

由于此项目已“插件化”，你可以直接通过以下指令安装：

```bash
/plugin marketplace add cosen1024/llm-wiki-skill
/plugin install llm-wiki-skill@cosen1024/llm-wiki-skill
```

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

![LLM Wiki Architecture](https://images.javalearn.cn/blog/2026/04/ca4ced3ee79e5d70344731a61d1d7968.png)

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

![LLM Wiki Workflow](https://images.javalearn.cn/blog/2026/04/3a9c6c9b036cd38b527dc4bf9ee87dbc.png)

| Command | Action |
|---|---|
| `build wiki` | Initialize the structure and co-evolve the `CLAUDE.md` schema. |
| `ingest this` | Process a raw source and weave it into the wiki fabric. |
| `wiki query` | Ask questions and generate "flowback" artifacts. |
| `lint wiki` | Perform a health check: find gaps, contradictions, and orphans. |

## 🌟 Best Practices

- **Flowback is magic**: Always file valuable query results back into the wiki.
- **Just dump into raw/**: Don't worry about organization; let the LLM handle the structure.
- **Use Obsidian**: Use it as your viewer. The LLM writes, you browse.

## 🤝 Credits

![Karpathy's Vision](https://images.javalearn.cn/blog/2026/04/eeea3ed3aeb2783bbf055dcfc81d164b.png)

Inspired by [Andrej Karpathy's LLM Wiki concept](https://karpathy.ai/blog/wiki.html).

## 📄 License

MIT
