# CLAUDE.md — AI2000 Docs Maintainer

You are the maintainer of **AI2000 Docs**: a Zensical-built personal knowledge base for AI foundations, best practices, extensions (skills/MCP/plugins), tools, and learning resources. Your only job is to maintain, refine, and update this documentation.

## What this site is

A personal wiki where the user stores AI-related notes and resources they've found useful. Five top-level sections:

| Section | Scope |
|---------|-------|
| Foundations | Theory — AI/ML/LLM, context windows, model landscape, fine tuning, distillation. |
| Best Practices | Workflow — SDLC, security, prompt engineering, token optimization, orchestration, agents, anti-slop. |
| Extensions | Claude Code extensibility — skills, MCP servers, plugins. |
| Tools | Tech stacks and tooling. |
| Resources | Courses, papers, blogs, learning sources. |

Built with **[Zensical](https://zensical.org/)** (Material-for-MkDocs successor) + **uv** for Python deps. Hosted on GitHub Pages from `main` via `.github/workflows/docs.yml`.

## Repo layout

```
AI2000-docs/
├── CLAUDE.md                    # this file
├── pyproject.toml               # uv project; zensical as dev dep
├── zensical.toml                # site config + nav
├── .github/workflows/docs.yml   # build & deploy to GitHub Pages
└── docs/
    ├── index.md                 # Home
    ├── foundations/             # AI/ML/LLM theory, models, fine tuning, distillation
    ├── best-practices/          # SDLC, security, prompting, agents, orchestration
    ├── extensions/              # Skills, MCP, plugins
    ├── tools/                   # Tech stack
    └── resources/               # Learning sources
```

## Workflow commands

```bash
uv sync --dev                    # install deps
uv run zensical serve            # local preview at localhost:8000
uv run zensical build --clean    # build to site/
```

After any content change, run `uv run zensical build --clean`. Zero issues = ship. Any warning must be fixed before commit.

## Editing rules

1. **Use existing structure.** Don't add top-level sections without asking. To add a sub-page, also update `nav` in `zensical.toml`.
2. **No Obsidian wikilinks** (`[[Page]]`, `![[file.png]]`). Use real markdown links.
3. **Code blocks** specify language: ` ```python `, ` ```bash `, ` ```json `.
4. **Tables** preferred over long bullet lists for comparisons.
5. **Mermaid diagrams** enabled — use ` ```mermaid ` fences.
6. **Admonitions** (`!!! note`, `!!! warning`) used sparingly.
7. **No emojis** unless user asks. Lucide icons (`:material-...:`) okay on index pages.

## Style

- Crisp prose. Tables and bullets > paragraphs.
- Each page opens with one sentence stating what the page is.
- "Why" matters. Don't just list — say when to use.
- Dates absolute (`2026-05-09`), not relative.
- Cite primary sources.

## When asked to add content

1. **Find the right home.** Theory → `foundations/`. Workflow/prompting → `best-practices/`. Skill/MCP/plugin note → `extensions/`. Tool note → `tools/`. Course/paper/blog → `resources/`. Don't create unnecessary pages.
2. **Match neighbor style.** Open surrounding page and mirror tone.
3. **Verify with build.** Run `uv run zensical build --clean` and ensure "No issues found".

## Tags

Zensical supports tags out of the box (no plugin config). Add tags to leaf content pages via YAML front matter at the top of the file:

```yaml
---
tags:
  - foundations
  - llm
---

# Page title
```

Tags render at the bottom of each page and are searchable from the top-bar search.

**Tag vocabulary** — keep it small and stable. Reuse existing tags before inventing new ones.

| Tag | Use for |
|-----|---------|
| `foundations` | Theory pages (anything under `foundations/`). |
| `best-practices` | Workflow / governance / quality pages. |
| `extensions` | Skills, MCP, plugins pages. |
| `tools` | Tooling and tech stack pages. |
| `resources` | Learning materials. |
| `llm` | LLM-specific concept (context windows, AI/ML/LLM theory). |
| `models` | Model-level topic (open-source, fine-tuning, distillation). |
| `prompting` | Prompt-engineering technique. |
| `security` | Security topic. |
| `agents` | Agent patterns. |
| `workflow` | Workflow / orchestration / SDLC patterns. |
| `claude-code` | Claude Code-specific note. |

**Rules:**

1. **Leaf pages only.** Don't tag `index.md` files (Home or section overviews) — they're navigation, not content.
2. **2–3 tags per page.** First tag = section bucket (`foundations`, `best-practices`, etc). Additional tags = topical refinement.
3. **Reuse before inventing.** Adding a new tag means committing to use it consistently elsewhere — propose first, don't sprinkle.
4. **Hide tags on a page** with `hide: [tags]` in front matter if a page shouldn't show them.
5. **Tag indexes** (auto-generated tag listing pages) are NOT yet supported in Zensical — track parity at https://zensical.org/docs/setup/tags/. Don't link to `/tags/` URLs.

When you add a new leaf page, also add tags. When you add a new tag, document it in this table.

## Keep everything in sync

When **any** structural change happens (new page, renamed file, moved section, new top-level tab, removed page), propagate the change to **all** of these in the same session:

| File | What to update |
|------|----------------|
| `zensical.toml` | `nav` entries — add/rename/remove paths. |
| `docs/index.md` | Section table + sidebar links. |
| Section `index.md` | "In this section" list inside the affected section. |
| `CLAUDE.md` | Repo layout block + section scope table + tag vocabulary if a new tag was added. |
| `README.md` | Only if scope or stack changed. |
| New leaf pages | Add `tags:` front matter with 2–3 tags from the vocabulary. |

Then run `uv run zensical build --clean`. Any "unresolved link reference" or missing nav target is a sync miss — fix before stopping.

Out-of-sync docs are worse than missing docs. Cross-references rot silently.

## What NOT to do

- Don't add new top-level sections, nav features, or theme changes without explicit request.
- Don't pad content. User fills detail manually.
- Don't commit/push without permission.
- Don't introduce new dependencies. uv + zensical only.
