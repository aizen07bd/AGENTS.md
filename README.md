# Cost-Aware AGENTS.md

AI coding agents are powerful, but they can waste tokens, repeat repository scans, run expensive commands too early, and drift across sessions.

This template is a **cost-aware AGENTS.md** designed to reduce unnecessary token usage, tool calls, rework, and verification cost while keeping agent behavior stable across projects.

---

## Korean

### 개요

`Cost-Aware AGENTS.md`는 AI 코딩 에이전트를 더 안정적이고 저비용으로 운영하기 위한 범용 지침 템플릿입니다.

기존 `AGENTS.md` 템플릿이 주로 “에이전트가 프로젝트 규칙을 잘 따르게 하기”에 초점을 둔다면, 이 템플릿은 다음을 1급 목표로 둡니다.

- 불필요한 토큰 사용 감소
- 반복적인 저장소 탐색 방지
- 검증 명령 비용 분류
- 확인된 명령만 사용
- 관련 파일만 읽고 수정
- 전체 테스트/빌드 남발 방지
- 사용자 변경사항 보호
- 위험 명령과 증거 제거 조치 방지

### 왜 필요한가

AI 코딩 에이전트는 세션마다 프로젝트 구조, 빌드 명령, 테스트 방식, 작업 규칙을 다시 추론하려고 합니다.

이 과정에서 다음 비용이 발생합니다.

- 토큰 비용
- 도구 호출 비용
- 잘못된 명령 실행으로 인한 재작업
- 과도한 테스트/빌드 실행 시간
- 불필요한 diff 리뷰 비용
- 사용자 변경사항 훼손 리스크

이 템플릿은 에이전트가 먼저 프로젝트 환경을 조사하고, 확인된 사실만 바탕으로 작업하도록 유도합니다.

### 핵심 원칙

- agent가 프로젝트 환경을 먼저 조사한다.
- agent가 확인되지 않은 명령을 만들지 않는다.
- agent가 가장 작은 관련 검증부터 실행한다.
- agent가 명령을 `cheap`, `normal`, `expensive`로 구분한다.
- agent가 관련 파일만 읽고 수정한다.
- agent가 반복적인 전체 저장소 탐색을 피한다.
- agent가 사용자 변경사항을 덮어쓰지 않는다.
- agent가 위험하거나 되돌리기 어려운 명령을 승인 없이 실행하지 않는다.
- agent가 증거 보존이 필요한 상황에서 cleanup 명령을 피한다.
- 세션이 바뀌어도 agent가 같은 작업 방식으로 이어간다.

### 포함된 섹션

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

### 사용 방법

1. 사용자는 프로젝트 루트에 `AGENTS.md` 템플릿을 추가합니다.
2. 이후 내용 채우기는 agent가 수행합니다.
3. agent는 프로젝트 환경을 조사합니다.
4. agent는 확인된 사실만으로 `Repository Map`과 `Commands`를 채웁니다.
5. agent는 빌드/테스트/린트/포맷 명령을 저장소에서 확인한 것만 기록합니다.
6. agent는 각 명령을 `cheap`, `normal`, `expensive`로 분류하고 비싼 명령의 실행 조건을 적습니다.
7. agent는 monorepo 여부를 확인하고, 필요한 경우에만 nested `AGENTS.md`를 제안합니다.
8. 사용자는 agent가 채운 내용을 검토하고 필요한 부분만 수정합니다.

### 추천 포지션

이 템플릿은 다음 상황에 특히 적합합니다.

- AI 코딩 도구 사용량/비용을 줄이고 싶은 경우
- 세션마다 같은 설명을 반복하고 싶지 않은 경우
- 에이전트가 테스트/빌드를 과하게 실행하는 경우
- 여러 프로젝트에서 일관된 agent 운영 규칙이 필요한 경우
- 증거 보존, 사용자 변경 보호, 위험 명령 차단이 중요한 경우

### 한 줄 요약

`Cost-Aware AGENTS.md`는 AI agent의 지능을 높이는 문서가 아니라, **같은 지능을 더 적은 비용과 더 적은 실수로 사용하게 만드는 운영 지침**입니다.

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
