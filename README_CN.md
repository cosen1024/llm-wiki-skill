# LLM Wiki Skill (中文版)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

基于 **Karpathy Wiki** 模式的知识库构建工具。专为 **Claude Code** 和 **Accio** 用户设计，让你的 AI 能够跨会话地进行知识积累。

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

## 📦 安装

这是一个适用于 Claude Code/Accio 的 Skill：

1. 克隆仓库到你的技能目录：
   ```bash
   git clone https://github.com/your-username/llm-wiki-skill.git
   ```
2. 在你的 AI Agent 中，加载并读取 `SKILL.md` 文件。

## 🌟 最佳实践

- **回流（Flowback）是灵魂**：养成习惯，将有价值的查询结果归档回 Wiki。
- **无脑丢入 raw/**：不要纠结文件夹分类，让 LLM 去处理结构。
- **配合 Obsidian**：把它作为你的浏览器。LLM 负责写，你负责看。

## 🤝 致谢

灵感源自 [Andrej Karpathy 的 LLM Wiki 构想](https://karpathy.ai/blog/wiki.html)。

## 📄 开源协议

MIT
