# AGENTS.md

Canonical source of truth for AI coding agents working in this repository. This
file is the single authority for project rules, workflow, conventions, and
skills policy. Pi reads it natively; Claude Code and Codex-compatible agents
read it through their respective adapters.

> Keep this file human-authored and concise. It is read by multiple agents
> (Pi, Claude Code, Codex, and any tool that can be pointed at it).

> **Adapting this file for a new project:** Replace the `## Project` section with
> real content and extend `## Conventions` and `## Skills` as the project needs.
> Universal rules (workflow, pull requests, writing style) live in `.pi/rules/`
> and are loaded automatically by Pi (via `pi-agent-kit`) and Claude Code (via
> `CLAUDE.md` `@`-references).

## Architecture

This repo is **Pi-native**. The canonical locations are:

```
AGENTS.md             # canonical project instructions for Pi and compatible agents
CLAUDE.md             # Claude Code adapter, points back to AGENTS.md and .pi/rules/
.pi/settings.json     # Pi project settings
.pi/rules/            # Universal rules (workflow, PRs, writing style) loaded by agents
.pi/skills/           # canonical Pi-native Agent Skills
.claude/skills -> ../.pi/skills  # symlink to canonical skills
.claude/rules -> ../.pi/rules    # symlink to canonical rules
.mcp.json             # shared MCP server config where supported
```

- **Instructions:** `AGENTS.md` is the single source of truth. `CLAUDE.md` is a
  thin adapter that delegates to `AGENTS.md`.
- **Skills:** Pi-native skills live canonically in `.pi/skills/`. Pi auto-discovers
  this directory. External harness skills (`~/.claude/skills`, `~/.codex/skills`)
  are loaded via `.pi/settings.json`. `.claude/skills/` and `.claude/rules/` are
  git-tracked symlinks to the canonical directories - no duplication.
- **MCP servers:** Shared in `.mcp.json`, read by Pi and Claude Code.

## Project

<!-- Describe the project: what it is, the tech stack, and key entry points. -->
TODO: Describe this project - purpose, tech stack, and where the important code lives.

## Conventions

- Follow existing code conventions; check sibling files before creating anything new.
- Prefer the project's own generators/scaffolding over hand-written boilerplate.
- Run the project's formatter and linter before finalizing changes.
- Every change must be covered by a test. Run the affected tests and make sure they pass.
- Do not change dependencies without approval.

## Skills

Reusable agent skills live in `.pi/skills/`. Pi auto-discovers them natively;
Claude Code accesses them through the symlink at `.claude/skills/`. Add a skill
as `.pi/skills/<name>/SKILL.md`.

Bundled skills:
- `initialize-agents-md` - adapts AGENTS.md to a concrete project
