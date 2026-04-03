# YoYo Design System

## Purpose

This repository is the shared working context for AI agents and human designers contributing to the YoYo design system, Figma-ready screens, and H5 campaign pages.

Use this file as the neutral, cross-agent operating guide.

## Source of Truth

- Product and design specs live in [`CLAUDE.md`](./CLAUDE.md).
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

## Agent Compatibility

This repo may be worked on by multiple agents, including Claude and Codex.

- `CLAUDE.md` should remain available for Claude.
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

- Claude command definition currently exists at [`.claude/commands/yoyo-design.md`](./.claude/commands/yoyo-design.md).
- Local Claude permissions currently exist at [`.claude/settings.local.json`](./.claude/settings.local.json).
- Untracked HTML files may represent work in progress and should not be deleted without confirmation.

## Recommended Structure

- `AGENTS.md`: shared agent workflow and handoff rules
- `CLAUDE.md`: detailed YoYo design spec and Claude compatibility
- `.claude/`: Claude-only commands and settings
- `WORKLOG.md`: optional active-task handoff log
