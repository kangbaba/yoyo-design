# YoYo Design for Codex

## Purpose

This file explains how Codex should work in this repository when the original workflow references Claude commands or Claude-only skills.

Read this file together with [`AGENTS.md`](./AGENTS.md) and [`CLAUDE.md`](./CLAUDE.md).

## What Codex Can Reuse Directly

- All product and design specs in [`CLAUDE.md`](./CLAUDE.md)
- All shared workflow and handoff rules in [`AGENTS.md`](./AGENTS.md)
- Existing HTML files, repo docs, and any work-in-progress assets

## What Is Claude-Specific

The following files are still useful as reference, but they are not native Codex command files:

- [`.claude/commands/yoyo-design.md`](./.claude/commands/yoyo-design.md)
- [`.claude/settings.local.json`](./.claude/settings.local.json)

Codex should read them as documentation, not as executable slash-command config.

## Command Translation

### `/yoyo-design`

Claude behavior:
- query YoYo design specs
- recommend components
- build screens in Figma
- review designs against the spec
- generate H5 campaign pages

Codex equivalent:
- ask directly in plain language, for example:
  - "Use the YoYo design spec to build a chat room screen"
  - "Review this page against the YoYo design system"
  - "Generate an H5 Ramadan campaign page based on the YoYo rules"

Codex should treat [`CLAUDE.md`](./CLAUDE.md) as the authoritative design spec for these tasks.

### `/figma-use` and `use_figma`

Claude behavior:
- relies on the Figma MCP server to inspect files, import components, and create or edit frames directly in Figma canvas

#### Figma MCP Setup (for Codex environments)

Install the Figma MCP server:

```bash
claude plugin install figma@claude-plugins-official
```

Or add manually:

```bash
claude mcp add --transport http figma https://mcp.figma.com/mcp
```

After installation, authenticate via `/plugin` → Installed → Figma → "Allow access" in browser.

Requirements: a full or development seat in Figma + edit or view-only permissions to the target file.

Key commands:
- `claude mcp list` — check connection status
- `claude mcp remove figma` — remove if needed

#### Codex equivalent

- If a Figma MCP, plugin, or internal design tool is available in the current Codex environment, use it.
- If no Figma tool is available, do not pretend direct Figma writes are possible.
- In that case, Codex should still do one of the following:
  - produce a precise screen spec for manual Figma construction
  - generate supporting HTML prototypes for visual review
  - prepare component lists, text content, spacing, and layout instructions
  - leave a clean handoff note describing what must be done in Figma

When direct Figma access is unavailable, Codex should be explicit about that limitation.

### `/deploy-to-vercel`

Claude behavior:
- deploys H5 pages directly

Codex equivalent:
- If deployment tooling is available in the environment, use it.
- If not, prepare the deployable HTML and provide the exact commands or handoff needed for deployment.

## Figma Workflow for Codex

When a teammate asks Codex to work on a Figma task, use this order:

1. Read [`AGENTS.md`](./AGENTS.md) for shared workflow.
2. Read [`CLAUDE.md`](./CLAUDE.md) for exact YoYo specs.
3. Read [`.claude/commands/yoyo-design.md`](./.claude/commands/yoyo-design.md) as reference for intended Figma workflow and component usage.
4. Check whether the current Codex environment actually has a Figma-capable tool.
5. If yes, perform the Figma task.
6. If not, produce a precise fallback deliverable instead of blocking.

## Required Codex Behavior

- All UI text must remain in English.
- Use exact design values from [`CLAUDE.md`](./CLAUDE.md).
- If the spec does not define something, say the current spec does not cover it.
- Prefer existing library components over rebuilding common elements.
- Do not claim to have modified Figma unless a real Figma-capable tool was available and used.

## Fallback Deliverables When Figma Access Is Missing

When Codex cannot edit Figma directly, the preferred fallback outputs are:

- a screen blueprint with frame size, layout structure, and component list
- exact text copy for all visible UI
- color, type, spacing, radius, and state rules from the YoYo spec
- HTML prototype when that helps review faster
- a short handoff note for a designer or another tool-enabled agent

## Prompt Patterns for Teammates

Use prompts like:

- "Read AGENTS.md, CODEX.md, and CLAUDE.md, then build an H5 event page."
- "Use the YoYo spec to review this design and list violations."
- "If direct Figma editing is unavailable, give me a complete Figma build spec instead."
- "Continue from the current repo state — read HANDOFF.md first."
- "Export a handoff.md for shifting task to claude."

## Maintenance Rule

When Claude-only workflow details are discovered, do one of the following:

- move the shared part into [`AGENTS.md`](./AGENTS.md) or [`CODEX.md`](./CODEX.md)
- leave the Claude-only part under [`.claude/`](./.claude/)

Do not force Codex users to depend on Claude slash commands for core repo workflows.
