# LLM Wiki Skill

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

[中文文档](#-为什么选择它) | [English Document](#-why-this)

---

## 🚀 为什么选择它？

**源自大神 Andrej Karpathy 的“第二大脑”构想。**

传统的 RAG（检索增强生成）只是“临时搬运工”，在你提问时临时抓取片段，没有积淀。而 Karpathy 提倡的 **LLM Wiki** 模式则是 **“知识编译器”**。

本项目将这一顶级思维转化为 **AI 原生技能 (AI-Native Skill)**：
- **大神理念**：摒弃复杂的向量数据库，让 LLM 像程序员维护代码库一样，持久化地维护你的 Markdown 维基。每一次摄取都是在织入知识，每一次查询都是在复利。
- **AI 原生实现**：这不仅是一个软件，更是一份**“大脑指令集”**。无需 Node/Python 环境，直接利用 Claude Code/Accio 的原生文件操作能力，实现最轻量、最智能的知识管理。

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

## 📦 安装与使用 (Installation & Usage)

你可以通过以下两种方式将此技能赋予你的 AI：

### 模式 A：插件安装 (推荐)
适用于 Claude Code/Accio 用户，一键集成到你的指令集：
```bash
/plugin marketplace add cosen1024/llm-wiki-skill
/plugin install llm-wiki-skill@cosen1024/llm-wiki-skill
```

### 模式 B：技能加载 (手动)
如果你不希望安装插件，可以手动克隆仓库，并让 AI 直接读取 `skills/llm-wiki.md` 的内容。

---

## 🚀 Why this?

**Inspired by Andrej Karpathy's "Second Brain" Vision.**

Standard RAG is just a "temporary courier" — it fetches fragments when you ask, but has no memory or accumulation. Karpathy's **LLM Wiki** pattern is a **"Knowledge Compiler"**.

This project transforms that high-level vision into an **AI-Native Skill**:
- **The Vision**: Move away from complex vector databases. Let the LLM maintain a persistent, interlinked Markdown Wiki as if it were maintaining a codebase. Every ingestion is an integration; every query is a compounding interest.
- **AI-Native Implementation**: This is not just software; it's an **"Instruction Set for the Brain."** It leverages the native file-op capabilities of Claude Code/Accio directly, making it the most lightweight and intelligent way to manage knowledge.

## 📖 Usage Guide

After enabling the skill, interact with the AI using **natural language**:

### 1. Three-Step Quick Start
1.  **Initialize**: "Build a knowledge base for [Your Domain]."
2.  **Feed Sources**: Drop PDFs/articles into the `raw/` folder.
3.  **Ingest Knowledge**: "Ingest new materials and update the wiki."

### 2. Example Prompts
*   "Build a research wiki for 'Deep Learning Crack Detection'."
*   "Ingest the 3 new papers in the raw folder and update the index."
*   "Compare Algorithm A vs. Algorithm B in a table format based on the wiki."
*   "Lint my wiki to find contradictions or orphan concepts."

### 3. The Magic: Flowback
When the AI provides a brilliant analysis, simply say:
> "File this analysis back into the wiki's comparisons directory."

---

## 🤝 Credits

Inspired by [Andrej Karpathy's LLM Wiki concept](https://karpathy.ai/blog/wiki.html).

## 📄 License

MIT
