# AGENTS.md

## Purpose

This file keeps AI agents stable, low-cost, and consistent across coding projects. Agents must discover the current project environment before making changes and must avoid unnecessary token use, tool calls, broad rewrites, and repeated verification.

## Operating Mode

- Start by inspecting only the minimum files needed to understand the task.
- Discover the project stack, structure, and commands before editing.
- Fill or update project-specific sections automatically after discovery.
- Prefer small, scoped edits over broad rewrites.
- Use existing project patterns instead of inventing new ones.
- State assumptions when required context is missing.
- Do not invent build, test, lint, format, or run commands.
- Do not refactor, reformat, rename, or move files unless the user asks.
- Preserve user-authored changes.

## Instruction Scope

- Treat this file as the shared agent instruction source for the project.
- If tool-specific files exist, such as `CLAUDE.md`, `GEMINI.md`, `.cursorrules`, `.cursor/rules/*`, or `.github/copilot-instructions.md`, read them only when they are relevant to the active tool or task.
- If instructions conflict, follow the most specific instruction for the current directory and task.
- If a nested `AGENTS.md` exists closer to the files being edited, apply it in addition to this file.
- Keep global rules stable; store verified project-specific details in `Repository Map`, `Commands`, or generated local notes.

## Project Discovery

Before implementation, identify and use only verified project facts:

- Root files and directory layout.
- Package/build files: `package.json`, `pnpm-lock.yaml`, `yarn.lock`, `package-lock.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, `pom.xml`, `build.gradle`, `Makefile`, `Dockerfile`, `docker-compose.yml`, or equivalents.
- Source directories.
- Test directories.
- Documentation directories.
- Build, test, lint, format, and run commands.
- Frameworks, languages, package managers, and runtime versions.
- Existing style, naming, and architecture patterns.
- Expensive, destructive, or network-dependent commands.
- Existing agent instruction files and local overrides.

After discovery, update the sections below with verified facts. If a fact is not found, keep it as `Unknown` or `Not found`. Do not guess.

## Repository Map

The agent fills this section after discovery:

- Project type: `Unknown`
- Languages/frameworks: `Unknown`
- Package manager: `Unknown`
- Source directories: `Unknown`
- Test directories: `Unknown`
- Documentation directories: `Unknown`
- Build files: `Unknown`
- Local agent instruction files: `Unknown`

## Commands

- Build: `Unknown`
- Test: `Unknown`
- Lint: `Unknown`
- Format: `Unknown`
- Run/dev server: `Unknown`
- Cheap verification: file existence, targeted search, type-local inspection, focused unit test.
- Normal verification: package-level test, typecheck, lint, or build for the touched area.
- Expensive verification: full test suite, full build, container build, E2E suite, dependency install, large scan, migration, or network-heavy command.

Only record commands that are verified from repository files or user instructions. Label each command as `cheap`, `normal`, or `expensive`. Run the cheapest relevant verification first.

## Cost Control

- Prefer targeted file reads over whole-repository scans.
- Prefer one precise `rg` query over multiple broad searches.
- Do not run install, build, full test, container, or network-heavy commands unless they are needed for the task.
- Avoid repeated tool calls that return the same information.
- Cache discovered project facts in this file or a local project note when it reduces repeated discovery.
- Ask before starting long-running, expensive, or irreversible work.

## Work Rules

- Read before editing.
- Edit only files needed for the task.
- Prefer existing utilities, patterns, APIs, and conventions.
- Keep changes minimal but complete.
- Do not add dependencies unless necessary and justified.
- Do not perform broad formatting unless requested.
- Do not repeat failed approaches without new evidence.
- Do not keep re-reading the entire repository when targeted search is enough.
- Use `rg` or project-native search before slower alternatives.
- Keep notes and final summaries short and evidence-based.
- For large work, maintain a short task list with status.
- Record important decisions only when they affect future agent behavior.

## Change Limits

- Touch only files related to the current request.
- Do not rewrite unrelated code.
- Do not rename, move, or delete files unless explicitly required.
- Do not modify generated files unless the project expects it.
- Do not overwrite user changes.
- Do not change public APIs, schemas, migrations, or configuration defaults without clear need.
- Do not introduce new architecture layers unless they remove real complexity or match existing project patterns.

## Verification

- Verify the smallest meaningful scope first.
- Prefer targeted tests for touched files or modules.
- Run broader tests only when shared behavior, public API, build configuration, or cross-module contracts changed.
- If tests fail, inspect the failure and fix only related issues.
- If a command cannot be run, state why and provide the best available alternative verification.
- Do not run repeated full-suite checks without a new change or reason.
- Do not clean caches or delete build artifacts during investigation unless the user approves.

## Review Rules

- Review changed files before finishing.
- Check for unrelated diffs, accidental formatting churn, generated artifacts, and secret exposure.
- If reviewing code, lead with concrete risks and file references.
- Do not claim full verification when only inspection was performed.

## Safety

- Never expose, add, or commit secrets, API keys, passwords, or tokens.
- Do not run destructive commands such as `rm`, `git reset`, checkout-based rollback, database reset, cache clean, migration rollback, bulk delete, or force push unless explicitly approved by the user.
- Ask for user approval before running commands that may change external systems, production data, cloud resources, databases, credentials, permissions, billing, or deployment state.
- Ask for user approval before installing dependencies, downloading tools, using network-heavy commands, or executing remote scripts.
- Do not access files outside the project unless the task requires it and permission is available.
- Treat `.env`, credentials, private keys, tokens, production configs, and customer data as sensitive.
- Do not paste secrets, proprietary source, customer data, logs with credentials, or private configuration into external services unless the user explicitly approves.
- Do not change authentication, authorization, encryption, sandbox, permission, or security policy code without targeted verification.
- When diagnosing failures, preserve evidence before cleanup.
- Ask for approval before actions that are irreversible, costly, network-heavy, or may affect production systems.

## Multi-Project Use

- For a single repository, keep this file at the project root.
- For a monorepo, the agent should detect subprojects and propose nested `AGENTS.md` files only when commands, languages, or safety rules differ.
- For many repositories, keep common guardrails in a shared source and let agents generate repo-local sections from verified facts.
- Do not overwrite local project instructions during sync; show a diff first.
- The agent may suggest compatibility shims, such as `CLAUDE.md` or `GEMINI.md` pointing to `AGENTS.md`, when a tool does not read this file directly.

## Maintenance

- The agent should update this file when build/test commands, source layout, safety rules, or agent workflow changes.
- Remove obsolete commands instead of leaving conflicting instructions.
- Keep this file short enough to load every session.
- Move long explanations, experiments, and research notes into separate docs and link them only when needed.

## Handoff

End with a short summary containing:

- Changed files.
- Verification performed.
- Commands not run and why.
- Assumptions made.
- Remaining next step only when directly useful.
