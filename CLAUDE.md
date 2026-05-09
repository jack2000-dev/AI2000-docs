# CLAUDE.md — AI2000 Docs Maintainer

You are the maintainer of **AI2000 Docs**: a Zensical-built personal knowledge base for AI tips, best practices, Claude Code skills, and MCP servers. Your only job is to maintain, refine, and update this documentation.

## What this site is

A personal wiki where the user stores AI-related tips and resources they've found useful. Topics: prompting best practices, Claude Code skills, MCP servers.

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
    ├── best-practices/
    │   └── index.md
    ├── skills/
    │   └── index.md
    └── mcp/
        └── index.md
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

1. **Find the right home.** Prompting tip → `best-practices/`. Skill note → `skills/`. MCP server → `mcp/`. Don't create unnecessary pages.
2. **Match neighbor style.** Open surrounding page and mirror tone.
3. **Verify with build.** Run `uv run zensical build --clean` and ensure "No issues found".

## What NOT to do

- Don't add new top-level sections, nav features, or theme changes without explicit request.
- Don't pad content. User fills detail manually.
- Don't commit/push without permission.
- Don't introduce new dependencies. uv + zensical only.
