# Cost-Aware AGENTS.md

AI coding agents are powerful, but they can waste tokens, repeat repository scans, run expensive commands too early, and drift across sessions.

This template is a **cost-aware AGENTS.md** designed to reduce unnecessary token usage, tool calls, rework, and verification cost while keeping agent behavior stable across projects.

---

## English

### Overview

`Cost-Aware AGENTS.md` is a general-purpose instruction template for running AI coding agents more reliably and with lower waste.

Many agent instruction files focus on making agents follow project rules. This template makes **cost control** a first-class goal.

It is designed to reduce:

- unnecessary token usage
- repeated repository scans
- guessed commands
- excessive builds and test runs
- broad rewrites
- unrelated diffs
- rework
- risky commands
- accidental damage to user changes

### Why This Exists

AI coding agents often re-discover the same project facts every session:

- repository layout
- package manager
- build commands
- test commands
- lint/format commands
- project conventions
- verification strategy

That repeated discovery is not free. It costs tokens, tool calls, runtime, review effort, and sometimes project safety.

This template instructs agents to discover the project environment once, record verified facts, and prefer the cheapest meaningful verification first.

### Core Principles

- The agent discovers the project environment before editing.
- The agent does not invent commands.
- The agent reads only the files needed for the task.
- The agent prefers small, scoped edits.
- The agent uses existing project patterns.
- The agent classifies commands as `cheap`, `normal`, or `expensive`.
- The agent runs the cheapest relevant verification first.
- The agent avoids repeated full-suite checks.
- The agent preserves user-authored changes.
- The agent avoids destructive or irreversible commands without approval.
- The agent preserves evidence during investigations.
- The agent keeps handoffs short and useful.

### Sections Included

- `Purpose`
- `Operating Mode`
- `Instruction Scope`
- `Project Discovery`
- `Repository Map`
- `Commands`
- `Cost Control`
- `Work Rules`
- `Change Limits`
- `Verification`
- `Review Rules`
- `Safety`
- `Multi-Project Use`
- `Maintenance`
- `Handoff`

### How To Use

1. The user copies the template into the project root as `AGENTS.md`.
2. The agent fills the project-specific sections.
3. The agent inspects the project environment.
4. The agent fills `Repository Map` and `Commands` using only verified facts.
5. The agent records build, test, lint, and format commands only when they are confirmed from repository files or user instructions.
6. The agent classifies each command as `cheap`, `normal`, or `expensive` and documents when expensive commands should run.
7. The agent checks whether the repository is a monorepo and suggests nested `AGENTS.md` files only when subprojects have different stacks, commands, or safety rules.
8. The user reviews the agent-filled sections and adjusts only what is necessary.
9. The user may add compatibility shims such as `CLAUDE.md`, `GEMINI.md`, or Cursor rules if the agent tool does not read `AGENTS.md` directly.

### Best For

This template is useful when:

- AI usage has token or rate limits.
- Full test suites are expensive.
- Agents repeatedly inspect the same files.
- Agents often guess commands.
- User changes must be protected.
- Multiple AI coding tools are used in the same project.
- You want consistent behavior across sessions.

### Positioning

Most agent instruction files optimize for instruction completeness.

This template optimizes for:

- token budget
- tool-call reduction
- verification cost
- scoped editing
- evidence preservation
- repeatable handoff

### One-Line Summary

`Cost-Aware AGENTS.md` does not make the model smarter. It helps the same model produce more useful work with fewer tokens, fewer tool calls, and fewer avoidable mistakes.
