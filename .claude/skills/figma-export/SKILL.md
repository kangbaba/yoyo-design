---
name: figma-export
description: Export assets, icons, screenshots, or visual references FROM existing Figma designs. Use when user asks to "export", "screenshot", "download", "save as PNG/SVG", or otherwise retrieve visual output from a Figma file. NOT for building or editing designs — use /yoyo-design for those.
---

# Figma Export Skill

> **Frequency note:** Designers on this project rarely export assets themselves — devs typically handle it. This skill exists so when an export *is* requested, the work uses the fast path instead of being routed through `use_figma`.

## When to use this skill

Trigger on any of these:
- "export this icon / asset / frame / section"
- "screenshot this", "save as PNG/SVG", "download these"
- "give me the image of …", "extract assets from …"

**Do NOT use this skill for:**
- Building, editing, modifying, or creating in Figma → use `/yoyo-design` + `use_figma`
- Inspecting design system tokens / specs → use `/yoyo-design`

## Tool routing — direct endpoints only

| Task | Tool |
|------|------|
| List children of a section/frame to find what to export | `mcp__figma-remote-mcp__get_metadata` |
| Export PNG / screenshot a node | `mcp__figma-remote-mcp__get_screenshot` |
| Inspect a node + get code/metadata alongside the visual | `mcp__figma-remote-mcp__get_design_context` |

**Never** route exports through `mcp__figma-remote-mcp__use_figma`. Plugin execution is stateful and multi-step, much slower than the dedicated read endpoints. `use_figma` is for **writes only**.

## URL parsing

Extract `fileKey` and `nodeId` from the user's Figma URL:
- `figma.com/design/:fileKey/:fileName?node-id=39-2` → `fileKey = :fileKey`, `nodeId = 39:2` (convert `-` to `:`)
- `figma.com/design/:fileKey/branch/:branchKey/:fileName` → use `branchKey` as `fileKey`

## Multi-asset workflow (validated)

For batch requests like "export all icons in this section":

### 1. Discover — single `get_metadata` call

Call `get_metadata` once on the parent section/frame. Filter children by name pattern (e.g. anything starting with `icon/`) and select the target nodes.

For component sets with state variants (Default, Disabled, Hover, etc.), pick each variant's node ID separately if you want one PNG per state.

### 2. Render — parallel `get_screenshot` calls

Issue **all** `get_screenshot` calls in a single message (one tool call per node). Each returns a short-lived PNG URL.

### 3. Download — parallel `curl` in one Bash command

```bash
cd <destination> && \
curl -s -o icon-chevron-up.png "$url1" & \
curl -s -o icon-chevron-down.png "$url2" & \
...
wait && ls -la <destination>
```

### 4. Naming convention

- Use the Figma node name, not the asset UUID
- Lowercase, hyphenated: `icon/chevron-up` → `icon-chevron-up.png`
- For variant states, suffix with state name: `icon-plus-default.png`, `icon-plus-disabled.png`

## Render size — important caveat

`get_screenshot` returns at canvas-native size by default. The `maxDimension` parameter only scales **down**, never up.

- A 48×48 icon will return as a 48×48 PNG even if `maxDimension=192`
- For higher-density assets (2x/3x for retina/code use), raster PNG cannot deliver — offer **SVG via `use_figma`** as the alternative (true vector, scales infinitely)

If the user needs production-grade assets and the native size is small, ask whether they want SVG instead before dumping low-res PNGs.

## Destination folder

If the user specifies a folder (e.g. "to ~/Desktop/test"), use it. Verify it exists before downloading.

If unspecified, ask before downloading — don't guess.
