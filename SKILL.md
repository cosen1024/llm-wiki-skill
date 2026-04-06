---
name: llm-wiki-skill
description: "Build and maintain LLM-powered personal knowledge bases using the Karpathy Wiki pattern. The LLM incrementally compiles raw sources into a persistent, interlinked markdown wiki, not RAG. Trigger: 'build wiki', 'init wiki', 'ingest', 'process source', 'wiki query', 'lint wiki', 'health check', 'knowledge base', '知识库', '整理', '摄取'."
---

# LLM Wiki Skill

Personal knowledge base where the LLM is the sole maintainer. Human feeds sources and asks questions. LLM compiles, cross-references, and maintains everything.

## Core Idea

**This is NOT RAG.** RAG re-derives knowledge from scratch on every query — no accumulation. Here, the LLM **incrementally compiles** raw sources into a persistent, interlinked wiki. Knowledge is built once and kept current. The wiki is a compounding artifact: every source added and every question asked makes it richer.

- **Human's two jobs:** Feed raw materials. Ask good questions.
- **LLM's job:** Everything else — summarize, cross-reference, file, maintain, lint.
- **The wiki:** A living, compiled artifact that only grows.

> Obsidian is the IDE. The LLM is the programmer. The wiki is the codebase.

---

## Architecture

### Three Content Layers + Schema

```
{vault}/
├── raw/              # Layer 1: Human feeds. IMMUTABLE. LLM reads, NEVER writes.
│   └── ...           # Articles, papers, notes, images, repos — 无脑丢进去
├── wiki/             # Layer 2: LLM maintains entirely. Human reads/browses.
│   ├── CLAUDE.md         # ★ Schema: domain config, conventions, workflows
│   ├── index.md          # Content catalog — LLM's navigation map
│   ├── log.md            # Chronological ops log (append-only)
│   ├── overview.md       # High-level synthesis of the entire knowledge base
│   ├── sources/          # One summary per raw source
│   ├── concepts/         # Concept articles (e.g., attention.md, rlhf.md)
│   ├── entities/         # People, tools, projects, orgs
│   └── comparisons/      # Cross-cutting analyses
└── output/           # Layer 3: Query products. Valuable results → flow back to wiki/
    ├── reports/
    ├── slides/           # Marp format
    └── charts/           # matplotlib / visualization
```

**Iron rules:**
1. `raw/` is **immutable** — the LLM NEVER modifies source files
2. `wiki/` is **LLM-owned** — human reads/browses, LLM writes everything
3. `output/` → wiki/ **flowback** is the compounding mechanism (最关键的一步)

### The Schema: wiki/CLAUDE.md

The most important file. It tells future LLM sessions how THIS specific wiki works:
- Domain scope and purpose
- Page type definitions with frontmatter conventions
- Naming rules and directory organization
- Ingest workflow tuned to the source types
- Output format preferences
- Domain-specific conventions discovered over time

**The schema is co-evolved** — human and LLM update it together as they discover what works. The skill teaches the general pattern; the schema governs the specific wiki.

### Two Navigation Files

- **`index.md`** — Content-oriented catalog of every wiki page with one-line summaries, organized by type. The LLM reads this FIRST on any operation. Updated on every ingest.
- **`log.md`** — Chronological, append-only timeline. Format: `## [YYYY-MM-DD] {op} | {title}`. Parseable with `grep "^## \[" log.md`. Shows what happened when.

---

## Operations

### 1. Init

**Trigger:** "build wiki", "init wiki", "搭建知识库", or any request to create a knowledge base.

1. **Understand the domain** — Ask: What topic/purpose? (research, personal, book notes, business intelligence?) What sources do you have? What outputs do you care about?
2. **Create directory structure** — Adapt subdirectories to the domain. A book wiki might use `wiki/characters/`, `wiki/themes/`, `wiki/chapters/` instead of generic categories. A research wiki might add `wiki/methods/`, `wiki/datasets/`.
3. **Generate `wiki/CLAUDE.md`** — Domain-specific schema including:
   - Wiki purpose and scope statement
   - Page types for this domain with expected frontmatter fields
   - Naming conventions
   - Ingest workflow specifics (how to handle this domain's source types)
   - Output format preferences
   - Any domain-specific rules
4. **Generate `wiki/index.md`** — Empty catalog with sections matching wiki subdirectories
5. **Generate `wiki/log.md`** — First entry: initialization
6. **Generate `wiki/overview.md`** — Placeholder awaiting first source
7. **Recommend setup:**
   - Obsidian Web Clipper for clipping articles → `raw/`
   - Set Obsidian attachment folder to `raw/assets/`
   - `git init` for version history
   - Drop first source and say "ingest this"

### 2. Ingest

**Trigger:** "ingest this", "process this", "摄取", or referencing a new source to add.

**Principle:** One source typically touches 5–15 wiki pages. The LLM reads it, extracts knowledge, and weaves it into the existing wiki fabric.

**Single source:**
1. Read the source thoroughly
2. Discuss key takeaways with user (3–5 bullets)
3. Create summary page in `wiki/sources/` — frontmatter (type, title, source_path, date_ingested, tags, key_concepts, key_entities), summary, key takeaways, connections via `[[wikilinks]]`
4. For each significant concept → create or **update** page in `wiki/concepts/`, adding new information and backlinks
5. For each significant entity → create or **update** page in `wiki/entities/`
6. Update `wiki/index.md` with all new/changed pages
7. Update `wiki/overview.md` if the big picture shifts
8. Append to `wiki/log.md`: `## [date] ingest | {title}` with source path, pages created/updated

**Batch** ("ingest all", "批量摄取"):
- Cross-reference `log.md` to find un-ingested raw files
- Process each (skip discussion step in batch mode)
- Run mini-lint after all sources processed
- Report summary of what was added/updated

**Page conventions:**
- Every page: YAML frontmatter with `type`, `title`, `updated` at minimum
- All cross-references: `[[wikilinks]]` (enables Obsidian graph view)
- Filenames: lowercase with hyphens (`self-attention.md`, `andrej-karpathy.md`)
- Source pages link back to `raw/` path for traceability
- Concept/entity pages: Overview → Details → Sources → Related sections

### 3. Query

**Trigger:** User asks a question about wiki content.

**Principle:** Don't just answer — produce artifacts that compound. Guide users toward better questions: not "what does X say?" but "compare A vs B across dimension X, citing all sources."

1. Read `wiki/index.md` to locate relevant pages
2. Read those pages (work from compiled wiki, not raw sources)
3. Synthesize answer with `[[wikilink]]` citations
4. Choose output format:
   - Simple factual → chat response
   - Comparison → table or `wiki/comparisons/` page
   - Deep analysis → `output/reports/{topic}.md`
   - Presentation → `output/slides/{topic}.md` (Marp)
   - Visualization → `output/charts/` (matplotlib)
5. **Flowback prompt** — For any non-trivial output: "This is worth keeping — want me to file it into the wiki?" If yes: save to appropriate wiki directory, update index, update log. **This is the compounding mechanism** — explorations accumulate instead of vanishing into chat history.

### 4. Lint

**Trigger:** "lint wiki", "health check", "检查 wiki", or suggest after every ~10 ingests.

**Scan the entire wiki for:**
- Contradictions between pages
- Stale claims superseded by newer sources
- Orphan pages with no inbound links
- Concepts mentioned frequently but lacking dedicated pages
- Missing cross-references that should exist
- Data gaps fillable via web search
- Potential new connections and questions to investigate

**Output:** Report in `output/reports/lint-{date}.md`. Ask which issues to fix, then apply. Append to log.

**This is maintenance work humans abandon but LLMs excel at** — the LLM can read the entire wiki in one pass, spot inconsistencies across dozens of pages, and suggest questions the human hasn't thought to ask.

---

## Conventions

### Essential Rules
- **`[[Wikilinks]]`** for ALL cross-references — enables graph view and backlinks
- **YAML frontmatter** on every page: `type`, `title`, `updated` at minimum; domain-specific fields per schema
- **`raw/` is immutable** — absolute rule, the LLM never writes to it
- **Filenames:** lowercase-with-hyphens (source pages match raw filename)
- **The wiki is a git repo** — commit after significant operations for free version history

### Obsidian Setup (when asked)
1. **Web Clipper** extension → clips articles to `raw/articles/`
2. **Attachment folder** → Settings → Files and links → `raw/assets/`
3. **Download hotkey** → "Download attachments for current file" → Ctrl+Shift+D
4. **Graph View** → visualize structure, find hubs and orphans
5. **Marp plugin** → render slides | **Dataview plugin** → dynamic queries over frontmatter
6. Use Obsidian as a **viewer, not an editor** — you browse, the LLM writes

---

## Scale Guidance

| Scale | Navigation | Tooling |
|---|---|---|
| Small (<50 sources) | `index.md` alone | None needed |
| Medium (50–200) | `index.md` + search | [qmd](https://github.com/tobi/qmd): local BM25+vector search for .md |
| Large (200+) | Chunked index + search | Full search infra; consider synthetic data + finetuning |

---

## Key Tips

- **Just dump into raw/** — Don't overthink organization. Web pages, PDFs, screenshots, READMEs, podcast transcripts — anything potentially valuable. The LLM will structure it.
- **Flowback is the magic** — Every query result filed back makes future queries richer. Make this habitual.
- **Ask analytical questions** — Not "summarize this article" but "compare X and Y's approaches to Z, citing all sources and noting contradictions."
- **Co-evolve the schema** — Update `wiki/CLAUDE.md` as you discover what works. It's the most important file for cross-session continuity.
- **Let the LLM suggest questions** — After lint or ingest, the LLM often surfaces connections and gaps the human hasn't noticed. Follow these threads.
