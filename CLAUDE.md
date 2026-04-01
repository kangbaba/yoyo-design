# YoYo Design System

## Project Overview

YoYo is a social voice chat app for iOS and Android, targeting markets across the Middle East, Southeast Asia, South Asia, and beyond. Core features include voice chat rooms, private messaging, moments (social feed), family groups, in-app games (Ludo, Dominoes, Among Us, etc.), virtual gifts, and activities/events.

- **Platforms**: iOS, Android (native) + H5 (mobile web campaigns)
- **Languages**: 16+ (English, Arabic, Indonesian, Malay, Urdu, Traditional/Simplified Chinese, Thai, Filipino, Bengali, Turkish, French, Japanese, Spanish, Vietnamese, Korean, and more)

## Repo Purpose

Design system specifications and AI-assisted prototyping for the YoYo design team. This repo is the source of truth for design specs and is used to generate Figma-ready screens and H5 campaign pages via Claude Code.

## Platform Variants

| | Mobile App (Figma) | H5 Campaign (Mobile Web) |
|---|---|---|
| Base width | 720px | 750px |
| Units | px (fixed, Figma-native) | rem/vw (responsive) |
| Primary output | Figma canvas | HTML file (deployable) |
| Secondary output | — | Figma canvas (on request) |
| Viewport | — | `<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">` |
| Safe area | — | Account for notch / home indicator via `env(safe-area-inset-*)` |
| Use case | App screens, features, flows | Campaign pages, event pages, promotional H5 |

## Rules

- **All UI text must be in English.** No Chinese or other languages in any output. Translate all labels (e.g. "返回" → "Back", "提交" → "Submit").
- When answering spec questions, give **exact values only** — never say "approximately" or "about".
- If a value is not defined in this spec, say "current spec does not cover this" — do not guess.

## Design System

### 1. Color System

> Colors are also available as **paint styles** in the YoYo Figma library. Use `figma.importStyleByKeyAsync(key)` to import and apply via `node.fillStyleId = style.id`.

#### 1.1 Brand Colors (Primary)

| Name | Library Style | Value | Usage |
|------|--------------|-------|-------|
| Primary/Green-gradience | `675e65ef...` | `#78E349` → `#1DCBCC` (135°) | Top bars, primary buttons, accent elements |
| Primary/Green-solid | `42fcfaa6...` | `#29CC96` | Brand color text on white, secondary button border/text, selected tab |
| Text green-light | `e955d69d...` | `#D4F5EA` | Light tag backgrounds, own chat bubble bg |

#### 1.2 Text Colors

| Name | Library Style | Value | Usage |
|------|--------------|-------|-------|
| 333 (Text black) | `1b2abcd5...` | `#333333` | Primary body text on light backgrounds |
| 666 | `1d3a537f...` | `#666666` | Secondary text |
| 999 | `b114b91b...` | `#999999` | Hint text, tertiary button text/border |
| 000 80 | `1c1bd9f3...` | `#CCCCCC` | Disabled text, placeholder text |

#### 1.3 Functional Colors

| Name | Library Style | Value | Usage |
|------|--------------|-------|-------|
| red | `30e0a47b...` | `#FF6060` | Error, unread badge, hangup, strong alert |
| yellow | `7b7a7488...` | `#FFCE00` | Coins, rewards, highlight |
| VIP | `37f7ba0c...` | `#D1911D` → `#FFDE57` → `#D1911D` | VIP badge exclusive gold gradient |
| ai persona | `c1c9c988...` | `#AA88FF` | AI feature indicator, purple |

#### 1.4 Neutral Colors

| Name | Library Style | Value | Usage |
|------|--------------|-------|-------|
| 000 | `129a325d...` | `#000000` | Pure black, rarely used |
| 000 96 | `00f755e1...` | `#F5F5F5` | Light grey main background |
| 000 90 (line) | `e878c837...` | `#E6E6E6` | Divider lines |
| 000 50 | `aa18538b...` | `rgba(0,0,0,0.50)` | Semi-transparent overlay |
| fff | `8939f993...` | `#FFFFFF` | White, card/list background |
| fff 60 | `a4dc9ea1...` | `rgba(255,255,255,0.60)` | White 60% opacity for immersive text |

#### 1.5 Secondary Colors

| Name | Library Style | Value | Usage |
|------|--------------|-------|-------|
| Secondary/green | `005d9cd9...` | `#E1F9E3` | Family tag bg (Normal) |
| Secondary/blue | `e27a467c...` | `#DAF0F7` | Family tag bg (Bronze) |
| Secondary/purple | `f44e06a3...` | `#DBDEF7` | Family tag bg (Silver) |
| Secondary/gold | `ce3b4c47...` | `#FAF0D9` | Family tag bg (Gold) |

#### 1.6 Family Tag Text Colors

Normal: `#00B182` | Bronze: `#006FD2` | Silver: `#6F15D8` | Gold: `#CD1820`

#### 1.7 Noble Text Colors

Level 1: `#3FA54E` | Level 2: `#54CFF4` | Level 3: `#AA88FF` | Level 4: `#FF43C5` | Level 5: `#FF1717`

#### 1.8 Gradients

| Name | Library Style | Stops |
|------|--------------|-------|
| Blue gradient | `17f9e5dc...` | `#6A5EEF` → `#38AEFF` |
| Purple gradient | `de59937a...` | `#7736DA` → `#C943DD` |

#### 1.9 Room & Game Type Colors (gradients, 135°)

mlbb: `#8B75FF` → `#ABBAFF` | ludo: `#95B6FF` → `#74C7FF` | find friends: `#FFBD99` → `#FF749D` | dominoes: `#99E8C6` → `#86CFB6` | amoungus: `#FFE281` → `#FF9D49` | pubg: `#5DACE0` → `#B9D0FF` | bull&sheep: `#FFBB77` → `#F86A6A` | free fire: `#DDA75E` → `#F3DDBD` | roblox: `#39D1DD` → `#BFFFF1` | uno: `#D59070` → `#B35742` | video room: `#4D4D4D` → `#666666`

### 2. Typography

**Font:** Roboto | **Weights:** Medium (M) and Regular (R) for each size
**Line height:** Auto | **Letter spacing:** 0px | **Design base:** 720px width

| Size | Weight | Usage |
|------|--------|-------|
| 40px | M | Extra large number display (coin balance) |
| 36px | M/R | Large button text |
| 32px | M | Page main title (e.g. "Message") |
| 30px | M/R | Secondary large title |
| 28px | M | **Most used across the app**: body text, list titles, module titles, medium button text |
| 26px | M/R | Small module/card titles |
| 24px | R | List description text, small button text |
| 20px | R | Helper/description text |
| 16px | R | Smallest size: tag text, tab bar text |

### 3. Buttons

**Universal rule: Full pill radius (cornerRadius = height/2), text padding >= 24px**

#### 3.1 Sizes

| Size | Height | Font Size |
|------|--------|-----------|
| Large | 96px | 36px |
| Medium | 80px | 28px |
| Small | 64px | 28px |

#### 3.2 Style Hierarchy

| Level | Background | Text Color | Border | Usage |
|-------|-----------|------------|--------|-------|
| Primary | YoYo Green gradient | `#FFFFFF` | None | Core actions (confirm, submit, join) |
| Secondary | `#FFFFFF` | `#29CC96` | `#29CC96` | Secondary actions |
| Tertiary | `#FFFFFF` | `#999999` | `#999999` | Weak actions (skip, later) |
| Quaternary | `#FFFFFF` | `#333333` | None | Text-link style (more, view all) |

### 4. Spacing

**Base grid: 4px multiples**

| Usage | Value |
|-------|-------|
| Page left/right padding | 24px |
| List item spacing | 12-16px |
| Module spacing | 20-24px |
| Card inner padding | 12-16px |
| Icon-to-text spacing | 8px |
| Grid gap | 12px |

### 5. Corner Radius

| Element | Radius |
|---------|--------|
| Avatar | Full circle (50%) |
| Card | 16px |
| Button | Pill (height/2) |
| Tag / Badge | Pill |
| Input | Pill |
| Filter Tab | Pill |

### 6. Core Component Patterns

#### 6.1 Bottom Navigation Bar
- 5 Tabs: Home / Game / Moment / Message / Me
- Selected: green filled icon + green text (#29CC96)
- Unselected: grey line icon + grey text (#999)
- Supports unread red dot

#### 6.2 User Identity Tag System
Compound tag group that frequently appears next to usernames across the app:
- Level tag (Lv.1): small radius, grey background
- VIP tag: VIP gradient gold
- Noble tag: colors by level 1-5 (see 1.7)
- Family tag (YOYOFAM): color by family level (see 1.5/1.6)
- Verified tag (Official): green pill
- Role tag (AI Lover / Agency / Family): various colors

#### 6.3 Message List Item
Avatar + username (with tags) + message preview + time + unread red dot

#### 6.4 Room List Item
Room cover + room name + intro text + tags (flag, count, family, type) + online count

#### 6.5 Chat Bubbles
- Other person: left, light grey background rounded rect
- Self: right, light green (#D4F5EA) background
- Supports: text, voice bar (waveform + duration), sticker, image
- Translate button follows bubble

#### 6.6 Chat Room Seat Layout
- Host: top center, large avatar
- Guest seats: 5-column grid
- Empty seat: grey chair placeholder
- Dark purple gradient background (#7736DA → #C943DD, 135°)

#### 6.7 Item Shop Card
- 2-column grid layout
- Card: product preview + name + price tag (pill gradient button, currency icon + price + days)
- Top-left corner supports display tags

### 7. Scene-Specific Rules

#### 7.1 Immersive Pages
- Chat room: purple gradient background + semi-transparent overlays
- Audio call: blurred background + dark overlay, centered avatar + user info + bottom action buttons
- Video call: fullscreen video + top overlay info (username, tags, diamond count) + bottom toolbar
- Universal: white text (#FFFFFF) or white with opacity (rgba(255,255,255,0.60))

#### 7.2 Standard Pages
- Main page background: #F5F5F5, card/list white #FFFFFF
- Tertiary pages (pure content): #FFFFFF
- Section dividers: #E6E6E6
