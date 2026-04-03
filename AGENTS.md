# YoYo Design System

## Purpose

This repository is the shared working context for AI agents and human designers contributing to the YoYo design system, Figma-ready screens, and H5 campaign pages.

Use this file as the neutral, cross-agent operating guide.

## Source of Truth

- Product and design specs live in [`CLAUDE.md`](./CLAUDE.md).
- Codex-specific workflow notes live in [`CODEX.md`](./CODEX.md).
- Claude-specific commands and runtime notes live under [`.claude/`](./.claude/).
- If `AGENTS.md` and `CLAUDE.md` conflict, follow `CLAUDE.md` for design specs and exact values, and follow `AGENTS.md` for collaboration workflow and handoff.

## Project Overview

YoYo is a social voice chat app for iOS and Android, with supporting H5 campaign pages for mobile web. The repo is used for:

- design system specification
- AI-assisted prototyping
- Figma-oriented screen construction
- H5 campaign page generation

## Working Rules

- All UI text in outputs must be in English.
- When answering design spec questions, use exact values only.
- If a value is not defined in the spec, state that the current spec does not cover it.
- Preserve existing project files and user work. Do not overwrite or delete work unless explicitly requested.
- Prefer updating shared documentation over leaving important decisions only in chat.

## Output Modes

### Mobile App / Figma

- Base width: 720px
- Follow `CLAUDE.md` for colors, typography, spacing, radius, and component patterns.
- Prefer existing library components over rebuilding common UI from scratch.

### H5 Campaign / Mobile Web

- Base width: 750px
- Use responsive units appropriate for mobile web.
- Account for safe areas and mobile viewport behavior.
- Follow `CLAUDE.md` for brand and UI specs.

## Agent Priority and Handoff

**Primary agent: Claude (Claude Code).** Claude handles all tasks by default.

**Backup agent: Codex.** Codex takes over when Claude's token budget is running low or exhausted for the session, or when the user explicitly routes a task to Codex.

### How handoff works

1. When Claude is approaching token limits or the user says to switch, Claude writes a handoff note to `WORKLOG.md` covering: current task, files touched, what's done, what remains, and any decisions made.
2. Codex picks up from `WORKLOG.md` and continues the work.
3. When Codex finishes or the user switches back, Codex updates `WORKLOG.md` the same way.
4. Both agents must read `WORKLOG.md` at session start if it exists.

### Rules

- Neither agent should redo work the other already completed — check `WORKLOG.md` and git history first.
- Both agents follow the same design spec (`CLAUDE.md`) and shared workflow (`AGENTS.md`).
- If an agent disagrees with a prior decision, note it in `WORKLOG.md` and ask the user — don't silently override.

## Issue-to-Design Workflow

When the design leader sends an issue (design request, feature spec, campaign brief), agents follow this process:

### Step 1 — Analyze

Read the issue and produce a **plan**: what screens, components, or pages are needed, which specs apply, dependencies, and suggested order of work.

### Step 2 — Break down

Split the plan into **individual tasks** — each task is one reviewable deliverable (e.g., one screen, one component, one section of an H5 page).

### Step 3 — Review

Present the plan and task list to the design leader for approval. Wait for sign-off or adjustments before executing.

### Step 4 — Execute

Work through tasks one by one. Mark each task complete as it's finished so progress is visible.

### Step 5 — Deliver

When all tasks are done, summarize what was built and flag anything that needs the design leader's final review.

### Guidelines

- Skip this process for quick asks (one-off spec questions, small tweaks). Just do it.
- Use this process for anything with 3+ deliverables or cross-screen scope.
- Plans are living documents — if something changes mid-task, update the plan rather than starting over.
- If handing off to the other agent mid-issue, the task list and plan carry over via `WORKLOG.md`.

## Agent Compatibility

This repo may be worked on by multiple agents, including Claude and Codex.

- `CLAUDE.md` should remain available for Claude.
- `CODEX.md` should describe how Codex translates Claude-specific workflows into Codex-friendly execution.
- `AGENTS.md` should contain shared instructions that any agent can read.
- Tool-specific instructions should stay in tool-specific files rather than in shared operating docs.
- If an agent cannot access a tool mentioned in repo docs, it should still follow the product and design intent and clearly state the tool limitation.

## Handoff Protocol

When stopping work or switching agents, leave durable context in the repo whenever practical.

Preferred handoff items:

- current task
- expected outcome
- files touched
- pending decisions
- blockers
- next recommended step

Recommended locations:

- `WORKLOG.md` for active task notes
- `README.md` for stable repo usage notes
- inline file comments only when they add lasting value

## Editing Expectations

- Keep changes focused on the task at hand.
- Avoid large speculative refactors.
- Do not remove agent-specific files unless the user asks.
- If introducing a new shared workflow, document it here first.

## Repo Notes

- Codex workflow notes currently exist at [`CODEX.md`](./CODEX.md).
- Claude command definition currently exists at [`.claude/commands/yoyo-design.md`](./.claude/commands/yoyo-design.md).
- Local Claude permissions currently exist at [`.claude/settings.local.json`](./.claude/settings.local.json).
- Untracked HTML files may represent work in progress and should not be deleted without confirmation.

## Recommended Structure

- `AGENTS.md`: shared agent workflow and handoff rules
- `CODEX.md`: Codex translation layer for Claude-oriented workflows
- `CLAUDE.md`: detailed YoYo design spec and Claude compatibility
- `.claude/`: Claude-only commands and settings
- `WORKLOG.md`: optional active-task handoff log
