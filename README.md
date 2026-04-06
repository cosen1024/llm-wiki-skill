# LLM Wiki Skill

A Codex/Claude-compatible skill for building personal knowledge bases using the **Karpathy Wiki** pattern, where the LLM incrementally compiles raw sources into a persistent, interlinked markdown wiki.

## What is this?

**This is NOT RAG.** RAG re-derives knowledge on every query. LLM Wiki **compiles** sources once into a persistent wiki that compounds over time. Every source added and every question asked makes it richer.

```
You (human)          LLM (maintainer)         Wiki (artifact)
    │                      │                        │
    ├── feed sources ─────►├── summarize ──────────►├── sources/
    │                      ├── cross-reference ────►├── concepts/
    │                      ├── link entities ──────►├── entities/
    ├── ask questions ────►├── synthesize answer    │
    │                      ├── flowback ──────────►├── comparisons/
    │                      │                        │
    │   browse in Obsidian ◄────────────────────────┤
```

**Roles:**
- **Human** — feed raw materials, ask good questions
- **LLM** — summarize, cross-reference, file, maintain, lint
- **Wiki** — a living, compiled artifact that only grows

> Obsidian is the IDE. The LLM is the programmer. The wiki is the codebase.

## Architecture

```
vault/
├── raw/          # Human feeds. Immutable. LLM never writes here.
├── wiki/         # LLM maintains entirely.
│   ├── CLAUDE.md     # Schema: domain config, conventions
│   ├── index.md      # Content catalog
│   ├── log.md        # Chronological ops log
│   ├── overview.md   # High-level synthesis
│   ├── sources/      # One summary per raw source
│   ├── concepts/     # Concept articles
│   ├── entities/     # People, tools, projects
│   └── comparisons/  # Cross-cutting analyses
└── output/       # Query products → valuable results flow back to wiki/
```

## Usage

This is a [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill. Install it and use natural language:

- `init wiki` / `build wiki` / `搭建知识库` — initialize wiki structure
- `ingest this` / `摄取` — process a source into the wiki
- `ingest all` / `批量摄取` — batch process all new sources
- `wiki query` — ask questions against compiled knowledge
- `lint wiki` / `health check` — check consistency and find gaps

## Key Operations

| Operation | What happens |
|---|---|
| **Ingest** | Read source → create summary → create/update concept & entity pages → update index |
| **Query** | Read index → find pages → synthesize answer → optionally flowback to wiki |
| **Flowback** | File query results back into wiki — the compounding mechanism |
| **Lint** | Find contradictions, orphans, missing pages, stale claims |

## Credits

Based on [Andrej Karpathy's LLM Wiki concept](https://karpathy.ai/blog/wiki.html) — the idea that LLMs should maintain persistent, compiled knowledge bases rather than re-deriving knowledge via RAG on every query.

## License

MIT
