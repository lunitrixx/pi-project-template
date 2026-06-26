---
name: initialize-agents-md
description: >-
  Initialize AGENTS.md after scaffolding from project-template-general.
  Detects tech stack, fills in Project section, extends Conventions with real
  commands, and lists relevant pi-agent-kit skills in the Skills section.
  Universal rules live in .pi/rules/ and must not be touched.
  Use when AGENTS.md still has the TODO placeholder, or when the user asks
  to "set up AGENTS.md" or "initialize the agent config".
---

# Initialize AGENTS.md for a new project

Adapts the template's `AGENTS.md` to a concrete project.

## When to use

Run once, right after scaffolding, when `AGENTS.md` still contains:

```
TODO: Describe this project - purpose, tech stack, and where the important code lives.
```

If that line is gone, confirm before re-running.

## Hard rules

1. **Never touch `.pi/rules/`.** Those are universal and loaded automatically.
2. **Never remove or weaken existing Conventions bullets.** Only append.
3. **Never delete the `## Skills` section.** Only update the skill list.
4. Do not invent facts. Verify from actual files or ask the user.

## Steps

1. **Confirm fresh template.** Check for the TODO placeholder. If absent, stop and ask.

2. **Detect the stack.** Check for package manifests and configs:
   - `package.json`, `composer.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `flake.nix`
   - CI under `.github/workflows/`, linter/formatter configs
   - Test runner and invocation

3. **Write `## Project`.** Replace TODO with 2-5 lines: what the project is, tech stack, key directories / entry points.

4. **Extend `## Conventions`.** Append concrete, verifiable commands (formatter, linter, test runner, generators). Keep the existing generic bullets.

5. **Configure `## Skills`.** Replace the bundled-skills list with the pi-agent-kit skills relevant to this project. Scan `~/.pi/agent/pi-agent-kit/skills/` (or wherever pi-agent-kit lives), pick the ones that apply, and list them with a one-line description. Keep the intro paragraph about `.pi/skills/`. Also note any project-specific skills already in `.pi/skills/`.

6. **Remove the template-only note.** Delete the blockquote starting `> **Adapting this file for a new project:**`. Keep the first blockquote (`Keep this file human-authored...`).

## Finish

- Verify `## Conventions` and `## Skills` are structurally intact.
- Confirm `.pi/rules/` was not touched.
- Summarize what was filled in.
