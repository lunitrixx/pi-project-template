# pi-project-template

A Pi-native starting point for repositories worked on by **multiple AI coding
agents** (Pi, Claude Code, Codex) - one source of truth, no config drift.

## Why

Multi-agent projects tend to accumulate duplicate config per tool
(`CLAUDE.md`, `.agents/`, `.codex/`, ...) that says the same thing in
different formats and drifts apart over time. This template keeps rules,
skills, and project instructions in one canonical location and lets every
agent reference it through its own thin adapter.

## Layout

```
AGENTS.md             # canonical project instructions for Pi and compatible agents
CLAUDE.md             # Claude Code adapter, delegates to AGENTS.md and .pi/rules/
.pi/settings.json     # Pi project settings
.pi/rules/            # Universal rules (workflow, PRs, writing style) for all agents
.pi/skills/           # canonical Pi-native Agent Skills
.claude/rules -> ../.pi/rules    # symlink to canonical rules
.claude/skills -> ../.pi/skills  # symlink to canonical skills
.mcp.json             # shared MCP server config where supported
.github/              # Collaboration scaffolding: PR template + issue templates
.vscode/settings.json # Shared VS Code defaults (LF, format on save)
.env.example          # Template for .env (committed; real .env is gitignored)
.gitignore            # Keeps personal/machine-specific config and secrets out
.gitattributes        # Cross-platform line-ending, diff, and binary normalization
.editorconfig         # Shared editor defaults (utf-8, LF, indentation, final newline)
LICENSE.md            # MIT license
```

## How it works

This repo is **Pi-native**. `AGENTS.md` is the single source of truth for
project rules. Pi reads it natively. Claude Code uses `CLAUDE.md` which
`@`-references `AGENTS.md` and follows symlinks to `.pi/rules/` and
`.pi/skills/`.

- **Instructions:** `AGENTS.md` holds project-specific context (description,
  conventions, skills). Universal rules live in `.pi/rules/`. Pi loads them
  via `pi-agent-kit`; Claude Code loads them through `CLAUDE.md` references.
- **Rules:** `.pi/rules/*.md` contain universal, always-applied rules
  (workflow, pull request policy, writing style). Keep them general -
  project-specific rules belong in `AGENTS.md`.
- **Skills:** Portable skills live in `.pi/skills/<name>/SKILL.md`. Pi
  auto-discovers this directory. External harness skills are loaded via
  `.pi/settings.json`. `.claude/skills/` is a git-tracked symlink to
  `.pi/skills/` - no adapter files, no duplication.
- **MCP servers:** Add entries to `.mcp.json` under `mcpServers`:

  ```json
  {
      "mcpServers": {
          "example-mcp": {
              "command": "npx",
              "args": ["-y", "@acme/example-mcp-server"]
          }
      }
  }
  ```

## Using this template

1. Create a new repo from this template (or copy the files in).
2. Let your agent run the **`initialize-agents-md`** skill - it detects the
   tech stack and fills in the `## Project` section of `AGENTS.md`.
3. Extend `## Conventions` and `## Skills` as the project needs.
4. Add MCP servers to `.mcp.json` and skills under `.pi/skills/`.
