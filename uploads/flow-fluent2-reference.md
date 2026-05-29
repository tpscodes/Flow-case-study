# Flow — Fluent 2 Design System Reference
**Tanishq Sardar · Windows 11 AI Concept**
*Built from fluent2.microsoft.design · May 2026*
*Structured in three sections: Visual Vocabulary · Material + Decision Rules · Token Application*

---

## HOW TO USE THIS FILE

**Image generation prompts (Gemini, ChatGPT, Midjourney):** Use Section 1 — Visual Vocabulary. Copy the relevant material description verbatim into your prompt. These descriptions are written in the language image AIs respond to.

**Design decisions (which material, which radius, which motion):** Use Section 2 — Material + Decision Rules. Each entry has a precise rule and a DO/DON'T.

**Code, prototype, CSS (Claude, Claude Code):** Use Section 3 — Token Application. All token names, values, and component patterns.

**Aligning Flow's philosophy to Fluent's:** Use Section 4 — Principles Alignment. Maps Flow's 6 design principles to Fluent's 4.

---

## SECTION 1 — VISUAL VOCABULARY
*For image generation prompts. Use these descriptions directly.*

### 1.1 The Fluent 2 Visual Language — Master Description
> "Microsoft Fluent 2 design language. Iridescent glass materials with soft rainbow light refractions on edges. Clean white or light grey backgrounds (#FAFAFA–#F5F5F5). Diffused, even illumination — no harsh shadows or dramatic contrast. Rounded corners (4–8px). Subtle depth through layered surfaces, not dramatic shadows. Colors are muted and purposeful — Communication Blue #0F6CBD for Microsoft UI, neutral greys #767676–#242424 for structure. Typography is Segoe UI Variable — clean, weight-differentiated, never decorative. Everything feels calm, precise, and trustworthy."

Use this paragraph as the base for every image prompt. Then append material-specific descriptions below.

---

### 1.2 Material Descriptions

#### SOLID MATERIAL
> "Solid, opaque surface. Uses color and elevation to define regions. Flat, smooth, matte finish — no transparency, no blur, no glass. Supports both light and dark modes. The background material for the main application chrome — stable, grounded, not calling attention to itself."

**When to use this description:** Dashboard screens, main application windows, settings panels, any persistent UI.

**Flow usage:** Flow application dashboard background = Solid with Mica (see below). Flow Overview screen, Contexts screen, History screen.

---

#### ACRYLIC MATERIAL
> "Semi-transparent frosted glass surface. 60% background blur visible through the surface, creating depth. Soft, diffused white-grey tint over the blur — not fully opaque. Rainbow iridescent light catches on the edges and corners at steep angles. The frosted effect makes background content visible but unreadable — you see shapes and colors, not text. Feels transient — this surface appears briefly, does its job, and disappears. Light and dark mode aware."

**When to use this description:** Prediction card, notification overlay, context menu, popover, tooltip, any surface that appears temporarily and dismisses.

**Flow usage:** The Flow prediction card (the core UI element). Context menus from the sidebar. Any transient overlay.

**Critical rule from official docs:** Acrylic is for transient, light-dismiss surfaces. It is NOT for persistent application chrome. If it stays on screen continuously, it should be Solid or Mica, not Acrylic.

---

#### MICA MATERIAL
> "Opaque surface, subtly tinted with the color of the user's current Windows desktop background — a very faint, desaturated echo of the wallpaper colors bleeding into the app chrome. When the window is active, the tint is visible. When the window is inactive or loses focus, the surface reverts to a flat neutral grey — the tinting disappears completely. This active/inactive state difference is a built-in Windows behavior, not a design choice. Feels like the app belongs to Windows — connected to the desktop environment."

**When to use this description:** App title bar, nav panel background, main application chrome — the permanent structure that wraps everything else.

**Flow usage:** Flow application window chrome (title bar area, sidebar nav background). The framing material — never the interactive content.

**Critical rule from official docs:** Mica tinting ONLY applies to active windows. Inactive Mica = neutral grey. This is non-negotiable Windows behavior — do not design Mica as if it's always tinted.

---

#### SMOKE MATERIAL
> "Dark semi-transparent overlay that dims everything beneath it — the entire screen goes darker and recedes into the background. The dimmed layer signals: something important needs your attention first, you cannot interact with what's behind me. Always dark (black at varying opacity) regardless of light or dark mode — smoke is not mode-aware. The dialog or modal sitting above the smoke is the focus point."

**When to use this description:** Modal dialogs, blocking confirmation screens, any interaction that requires the user to complete an action before returning to the main UI.

**Flow usage:** Destructive action confirmations ("Delete all Flow data?"). Critical onboarding gates. NOT for the prediction card — that is non-blocking and dismissable.

**Critical rule from official docs:** Smoke is ALWAYS backdrop black. It is NOT mode-aware. It is ONLY for blocking/modal interactions. The prediction card is explicitly NOT smoke because it is light-dismiss and non-blocking.

---

### 1.3 Illustration Style (for splash and onboarding screens)

Based on your existing illustration set — consistent visual language to maintain:

> "Microsoft Fluent 2 3D illustration style. Objects rendered as iridescent glass — semi-transparent with rainbow prismatic light refractions visible on surfaces and edges. Soft, even white studio lighting from above-left. White or very light grey background (#FFFFFF–#F5F5F5). Objects have physical weight and depth but remain clean and geometric — no organic textures, no noise. Color palette: soft purples, blues, cyan, with pearl-white and neutral grey. Shadow is soft and diffused, never dramatic. The overall feeling is calm precision — technology that is refined and trustworthy, not exciting or flashy."

**Flow brand color accent:** When incorporating Flow's iris purple (#6C5CF5) into an illustration, it appears as a glowing inner light source — a subtle purple luminescence emanating from within glass objects, not as a painted surface color.

---

### 1.4 Color Vocabulary for Prompts

| Color role | Hex | When to reference in prompts |
|---|---|---|
| Flow iris purple | #6C5CF5 | Prediction card, confidence bar, Flow brand moments ONLY |
| Flow violet | #B24BF5 | Secondary accent, gradient with iris |
| Flow cyan | #06B6D4 | Tertiary accent |
| Microsoft communication blue | #0067C0 | All Microsoft 365 app UI, buttons, active states, badges |
| Neutral dark | #242424 | Primary text |
| Neutral mid | #767676 | Secondary text, labels |
| Neutral light | #F5F5F5 | Background surfaces |
| Pure white | #FFFFFF | Cards, elevated surfaces |

**The two-color rule (non-negotiable):**
- `#0067C0` Microsoft blue = everything in the Flow application UI (buttons, links, active indicators, badges)
- `#6C5CF5` Flow iris purple = prediction card ONLY (confidence bar, action buttons, card glow)
- These must never appear together in the same UI element. The dashboard is Microsoft blue. The prediction card is iris purple.

---

## SECTION 2 — MATERIAL + DECISION RULES
*Precise rules for design decisions. Source: fluent2.microsoft.design/material*

### 2.1 Material Selection Table

| Surface type | Correct material | Reason |
|---|---|---|
| Flow app window chrome (title bar, nav) | Mica | Active window app chrome — Windows native behavior |
| Flow dashboard background | Solid | Persistent, non-transient main content area |
| Prediction card | Acrylic | Transient, light-dismiss overlay |
| Context menus / dropdowns | Acrylic | Transient, light-dismiss |
| Settings panels (persistent) | Solid | Permanent content area |
| "Delete all data" confirmation | Smoke + Solid dialog | Blocking modal interaction |
| Onboarding screens | Solid (app window) | Not transient — user must complete flow |
| Tooltips | Acrylic | Transient, appears briefly |

**The question to ask yourself before choosing a material:**
1. Is it transient and dismissable? → Acrylic
2. Is it the permanent app chrome/frame? → Mica
3. Is it blocking and requires completion before moving on? → Smoke
4. Is it everything else? → Solid

---

### 2.2 Elevation Rules
*Source: fluent2.microsoft.design/elevation*

Fluent shadows combine:
- **Key shadow**: Sharp, directional — defines the edge of an element
- **Ambient shadow**: Soft, diffused — implies distance from background

**Windows-specific rule:** Windows uses **strokes** instead of key shadows to outline objects. If you are designing for Windows specifically (which Flow is), use a subtle border/stroke for edge definition, not a key shadow.

| Element | Shadow token | CSS value |
|---|---|---|
| Resting card | shadow4 | `0 2px 4px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)` |
| Hover card | shadow8 | `0 4px 8px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)` |
| Prediction card (Acrylic, floating) | shadow16 | `0 8px 16px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)` |
| Dialog/modal | shadow28 | `0 14px 28px rgba(0,0,0,.24), 0 0 8px rgba(0,0,0,.2)` |

**Brand color elevation note:** When applying shadows to colored surfaces (like the Flow iris purple prediction card), the standard shadow values do not give the same visual impression as on neutral surfaces. Use the luminosity equation — in practice, increase the shadow opacity slightly on colored backgrounds to maintain the same perceived elevation.

---

### 2.3 Shape Rules
*Source: fluent2.microsoft.design/shapes*

**Three corner radius contexts:**
1. **Rectangular elements** (cards, panels, inputs): `borderRadiusMedium` (4px) to `borderRadiusXLarge` (8px)
2. **Flyout elements** (dropdowns, popovers, menus): `borderRadiusLarge` (6px)
3. **Pill/round elements** (badges, avatars, tags): `borderRadiusCircular` (10000px)

**DO NOT round corners when:**
- The component touches the screen edge (notification card anchored to bottom-right corner — the corner touching the screen edge should be 0px, the visible corners get radius)
- Rounding would create an awkward gap between two components sharing a container (e.g. split buttons)

**Flow application:** The prediction card appears bottom-right. The two corners touching the screen edges (bottom and right) should be 0px radius. The top-left corner gets the full radius. This is the correct Fluent 2 behavior.

---

### 2.4 Motion Rules
*Source: fluent2.microsoft.design/motion*

**Four motion principles (official):**
1. **Functional** — Every animation serves a purpose (orient, respond, give feedback). No decorative motion.
2. **Natural** — Duration and easing match the size and distance of the moving element. Larger elements take longer.
3. **Consistent** — Unified motion across Flow reinforces the Unmistakably Microsoft principle.
4. **Appealing** — Delightful moments draw people in — but sparingly.

**Duration scale for Flow:**
| Motion | Token | Value | Flow use case |
|---|---|---|---|
| Focus ring, button press | durationFaster | 100ms | Confidence bar pulse |
| Component state change | durationFast | 150ms | Card appear/dismiss |
| Most transitions | durationNormal | 200ms | Default for all transitions |
| Content entering | durationGentle | 250ms | Prediction card slide in |
| Drawer, sidebar | durationSlow | 300ms | Flow sidebar opening |
| Complex sequences | durationSlower | 400ms | Workspace switch animation |

**Easing:**
- Card appearing (entering screen): `cubic-bezier(0, 0, 0, 1)` — ease out, decelerates into place
- Card dismissed (leaving screen): `cubic-bezier(1, 0, 1, 1)` — ease in, accelerates out, doesn't linger
- Card moving within screen: `cubic-bezier(0.8, 0, 0.2, 1)` — ease in-out

**Critical rule:** Always include `prefers-reduced-motion` fallback. The prediction card must not animate at all if the user has reduced motion enabled in Windows.

---

### 2.5 Typography Rules
*Source: fluent2.microsoft.design/typography + skill file*

**Font stack for Windows (Flow):**
```
"Segoe UI Variable", "Segoe UI", system-ui, sans-serif
```
Your current CSS uses `"Figtree", "Segoe UI Variable", system-ui` — Figtree first means Windows users see Figtree, not Segoe UI. For the actual Windows app (React/Claude Code build), this should be reversed. For case study HTML (web-only): Figtree first is fine and probably looks better in a browser.

**Alignment rules (official):**
- Always baseline alignment for vertical rhythm
- Left-align for LTR — never right-align long blocks
- Center-align only for short callout text or to support another element
- Primary color on text = more prominence. Lighter neutral = de-emphasize.

**Contrast minimums (WCAG, non-negotiable):**
- Standard text (below 18.5px bold / 24px regular): 4.5:1 minimum
- Large text: 3:1 minimum
- Flow iris purple (#6C5CF5) on white (#FFFFFF): **contrast ratio 4.0:1** — this FAILS WCAG AA for body text. Only use iris purple on text at sizes 18.5px bold or larger, or against a darker background.

**Type ramp (full):**
| Token name | Size | Line height | Weight | Flow use |
|---|---|---|---|---|
| Caption2 | 10px | 14px | 400 | Eyebrow labels, timestamps |
| Caption1 | 12px | 16px | 400/600 | Card metadata, secondary labels |
| Body1 | 14px | 20px | 400/600/700 | Card body text, descriptions |
| Body2 | 16px | 22px | 400/600 | Slightly larger body, confirmation text |
| Subtitle2 | 20px | 28px | 600 | Section headings |
| Subtitle1 | 24px | 32px | 600 | Screen headings |
| Title3 | 28px | 36px | 600 | Major screen titles |

---

### 2.6 Color Rules
*Source: fluent2.microsoft.design/color*

**Three palettes:**
- **Neutral** — blacks, whites, greys — grounds the interface, used for surfaces, text, layout elements
- **Shared** — status colors (success green, warning amber, error red, info blue) — semantic meaning
- **Brand** — Flow iris #6C5CF5 (Flow identity) / Microsoft blue #0067C0 (Microsoft 365 identity)

**Windows interaction state rule (important and counterintuitive):**
> Windows interaction states treat color in REVERSE — controls get LIGHTER when interacted with (hover, press).
> This is the opposite of standard web convention where elements get darker on hover.
> If building for actual Windows, follow this rule. If building a web demo, standard web convention is fine.

**Color token structure:**
- **Global tokens**: Raw hex values — `#6C5CF5` directly stored
- **Alias tokens**: Semantic roles — `colorBrandBackground`, `colorNeutralBackground1` — these auto-adapt between light/dark mode
- **Never hardcode hex values** in production code. Always use alias tokens.

---

### 2.7 Layout Rules
*Source: fluent2.microsoft.design/layout*

**Base unit:** 4px. All spacing is a multiple of 4. Exceptions: 2px, 6px, 10px exist to align icons to the 4px grid.

**Spacing ramp:**
`2 · 4 · 6 · 8 · 10 · 12 · 16 · 20 · 24 · 28 · 32 · 36 · 40 · 48 · 52 · 56`

**Grid:** 12-column (divisible into halves, thirds, quarters, sixths)

**Desktop breakpoints (Flow is desktop-first):**
- `x-large`: 1024–1365px — standard laptop screen
- `xx-large`: 1366–1919px — HD monitor / most desktops
- `xxx-large`: 1920px+ — large monitors

**Proximity rule:** Elements in close proximity are perceived as related. Use spacing to create logical sections without graphical dividers (lines, etc.). This is how your current card designs work — proximity creates grouping, not borders.

**Hierarchy rule:** Elements with more space around them are perceived as higher in importance. This directly informs the prediction card — it should have generous padding/margin to signal its importance as the primary action.

---

## SECTION 3 — TOKEN APPLICATION
*For code, prototypes, CSS. Source: fluent2.microsoft.design skill file + official token docs*

### 3.1 Color Token Map — Light Theme

**Backgrounds (elevation order, lowest to highest):**
```
colorNeutralBackground1  → Page/canvas (#FFFFFF in light)
colorNeutralBackground2  → Cards, panels (#FAFAFA)
colorNeutralBackground3  → Nested containers (#F5F5F5)
colorNeutralBackground4  → Input fill, subtle surfaces (#F0F0F0)
colorNeutralBackground6  → Hover states on neutral
```

**Text:**
```
colorNeutralForeground1  → Primary text (#242424)
colorNeutralForeground2  → Secondary text (#424242)
colorNeutralForeground3  → Tertiary/placeholder (#767676)
colorNeutralForeground4  → Disabled text
```

**Brand (Flow iris):**
```
colorBrandBackground     → Flow iris purple fill (#6C5CF5) — prediction card only
colorBrandForeground1    → Flow iris on light surface — USE ONLY at 18px+ bold
colorBrandBackgroundHover
colorBrandBackgroundPressed
```

**Status:**
```
colorStatusSuccessBackground1 / colorStatusSuccessForeground1
colorStatusWarningBackground1 / colorStatusWarningForeground1
colorStatusDangerBackground1  / colorStatusDangerForeground1
colorStatusInfoBackground1    / colorStatusInfoForeground1
```

### 3.2 Spacing Token Map

**Horizontal and Vertical (identical values, different axis tokens):**
```
spacingHorizontalXXS → 2px
spacingHorizontalXS  → 4px
spacingHorizontalS   → 8px
spacingHorizontalM   → 12px
spacingHorizontalL   → 16px
spacingHorizontalXL  → 20px
spacingHorizontalXXL → 24px
spacingHorizontalXXXL → 32px
```

### 3.3 Border Radius Token Map

```
borderRadiusNone     → 0px   (screen-edge touching corners)
borderRadiusSmall    → 2px   (dense/compact)
borderRadiusMedium   → 4px   (buttons, inputs, default)
borderRadiusLarge    → 6px   (dialogs, panels, flyouts)
borderRadiusXLarge   → 8px   (cards, overlays, prediction card)
borderRadiusCircular → 10000px (avatars, badges, pills, confidence bar)
```

### 3.4 Shadow Token Map

```
shadow2  → 0 1px 2px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)   [resting cards]
shadow4  → 0 2px 4px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)   [hover cards]
shadow8  → 0 4px 8px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)   [dropdowns, menus]
shadow16 → 0 8px 16px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)  [prediction card]
shadow28 → 0 14px 28px rgba(0,0,0,.24), 0 0 8px rgba(0,0,0,.2)  [dialogs, modals]
shadow64 → 0 32px 64px rgba(0,0,0,.24), 0 0 8px rgba(0,0,0,.2)  [full panels]
```

### 3.5 Motion Token Map

```
durationUltraFast → 50ms
durationFaster    → 100ms
durationFast      → 150ms
durationNormal    → 200ms
durationGentle    → 250ms
durationSlow      → 300ms
durationSlower    → 400ms
durationUltraSlow → 500ms

Ease out (entering): cubic-bezier(0, 0, 0, 1)
Ease in (leaving):   cubic-bezier(1, 0, 1, 1)
Ease in-out (moving): cubic-bezier(0.8, 0, 0.2, 1)
Linear (looping):    linear
```

### 3.6 Component Quick Reference

**Button:**
```
height: 32px (medium/default), 24px (small), 40px (large)
border-radius: borderRadiusMedium (4px)
font-size: Body1 (14px)
font-weight: 600 (semibold)
Primary: colorBrandBackground fill, white text
Secondary: transparent, colorBrandStroke border + colorBrandForeground text
Subtle: no border/background, colorBrandForeground text
```

**Card:**
```
background: colorNeutralBackground1
border: 0.5px solid colorNeutralStroke1 (Windows uses strokes, not key shadows)
border-radius: borderRadiusXLarge (8px)
padding: spacingHorizontalXL (20px)
shadow: shadow4 resting, shadow8 on hover
```

**Input:**
```
background: colorNeutralBackground1
border: colorNeutralStroke1 (1px)
focused: colorBrandStroke1 bottom border (2px)
error: colorStatusDangerForeground1 label, colorStatusDangerBorder1 stroke
always pair with a visible label (no placeholder-only)
```

**Prediction card (Flow-specific):**
```
material: Acrylic (frosted glass, semi-transparent)
position: fixed, bottom-right
border-radius: borderRadiusXLarge (8px) top-left only; 0px for screen-touching corners
shadow: shadow16 (floating overlay)
brand color: iris purple (#6C5CF5) — NOT Microsoft blue
confidence bar: borderRadiusCircular (pill shape)
```

---

## SECTION 4 — PRINCIPLES ALIGNMENT
*How Flow's 6 design principles map to Fluent 2's 4 official principles*

### Fluent 2 Official Principles (source: fluent2.microsoft.design/design-principles)

**1. Natural on every platform**
> Adapt to the device and build off the familiar. 80% native platform patterns, 20% signature experiences. Functional: layout adapts, platform-aware. Emotional: intuitive and expected, creates reliability and trust.

**2. Built for focus**
> Stay in the flow. Technology shouldn't get in the way. Functional: products perform, enable people on their terms. Emotional: less clutter, more calm and confidence.

**3. One for all, all for one**
> Be inclusive. Consider, learn, and reflect a range of perspectives. Functional: diverse input makes better solutions. Emotional: when you're included, you feel like you belong.

**4. Unmistakably Microsoft**
> Feel like one Microsoft. Signature experiences connect products. Functional: color, sound, illustration, icons create familiarity. Emotional: a little personality goes a long way.

---

### Flow's 6 Principles Mapped

| Flow principle | Fluent principle | Alignment |
|---|---|---|
| Transparency first | Built for focus | Technology shouldn't get in the way — showing the prediction before acting is the mechanism for this |
| Trust earned incrementally | Natural on every platform | Building off familiar patterns; the confidence bar is the expected interaction model |
| Control is non-negotiable | One for all, all for one | Inclusive design — users with different trust levels and comfort with AI all need to feel respected |
| Ambient, not intrusive | Built for focus | Less clutter and noise — the prediction card earns its presence, doesn't announce itself |
| Partner not replacement | Unmistakably Microsoft | Signature Microsoft intelligence that connects experiences; Flow is the connective tissue |
| Windows freedom respected | Natural on every platform | 80% native Windows patterns; Flow doesn't add new menus or modes unless the user asks |

**The alignment is genuine, not forced.** Flow's design philosophy is a specific application of Fluent 2's broader principles to the context of ambient AI.

---

## SECTION 5 — FLOW-SPECIFIC ISSUES TO FIX

These are discrepancies found by cross-checking your current project files against the official Fluent 2 docs.

### Issue 1 — Iris purple contrast on text ⚠️ NEEDS FIX
**Problem:** #6C5CF5 on white (#FFFFFF) has a contrast ratio of approximately 4.0:1 — below the 4.5:1 WCAG AA minimum for body text.
**Current usage in files:** The discover-define HTML and personas HTML use iris as a text color on white backgrounds for labels and body text.
**Fix:** Use iris purple on text ONLY at 18px bold or larger. For small labels, use `--iris-700: #4133A8` instead — this has approximately 6.5:1 contrast on white and passes WCAG AA.

### Issue 2 — Prediction card material framing ⚠️ CHECK
**Problem:** The session document calls the notification/prediction card "Acrylic surface" but notes it appears over the raw Windows desktop. Per Fluent 2 docs, Acrylic is correct for this case — but the card corners touching the screen edge should be 0px radius (not rounded), per the shapes spec. Current prototype may have all four corners rounded.
**Fix:** Bottom-right corners = 0px. Top-left and potentially top-right corners = 8px (borderRadiusXLarge).

### Issue 3 — Font stack in HTML files ⚠️ MINOR
**Problem:** HTML files use `"Figtree", "Segoe UI Variable"` — Figtree loads first, so Windows users see Figtree not Segoe UI.
**Decision:** Fine for case study web page (Figtree reads better in browser). Must be corrected to `"Segoe UI Variable"` first in the actual React/Fluent UI app.

### Issue 4 — Research errors (previously flagged, still open) 🔴 MUST FIX BEFORE CASE STUDY
| Error | Current state | Correct state |
|---|---|---|
| 23-min figure | Cited as CHI 2005 | Mark, Gudith & Klocke, CHI **2008** — "The Cost of Interrupted Work" |
| 40% time lost | Attributed to HBR | HBR figure is 9% / 4 hours per week. 40% is APA research on multitasking — separate claim, separate source |
| 26% higher stress | No verified source | Cut the stat or find primary source — currently unfounded |
| 73% trust | Framed as statistic in main Context doc | Must be framed as observed pattern everywhere, not a data point |

---

## SECTION 6 — IMAGE PROMPT TEMPLATES
*Ready-to-use prompt fragments for generating Flow screens with Gemini or ChatGPT*

### For prediction card illustrations:
> "Microsoft Fluent 2 design system. Windows 11 desktop. Bottom-right corner of screen shows a frosted glass notification card — Acrylic material, semi-transparent with soft background blur, iridescent rainbow light catching on the glass edge. The card shows a workspace switching prediction: context name, confidence bar in iris purple (#6C5CF5), app icons in a row (Word, Outlook, Figma), two action buttons (Switch/Dismiss). The card has white background with subtle purple glow from the confidence bar. Surrounding desktop is blurred — Figma and Outlook windows partially visible. Windows 11 taskbar at bottom. Light theme. Clean, calm, trustworthy."

### For dashboard screens:
> "Microsoft Fluent 2 design system. Windows application window with Mica material — app chrome subtly tinted with desktop background color, active window state. Inside: clean white cards (Solid material, shadow4 elevation), 12-column layout, Communication Blue #0067C0 for active states and buttons. Left sidebar navigation with 5 items. Main content area shows context cards with app icon rows and three-dot confidence indicators. Segoe UI Variable typography, sentence case. Calm, professional, not flashy. Light theme."

### For onboarding illustrations:
> "Microsoft Fluent 2 3D illustration style. Objects rendered as iridescent glass — semi-transparent with rainbow prismatic light refractions. White background. Even, soft studio lighting. Purple inner glow (#6C5CF5) emanating from within glass objects. Clean geometric forms — folders, panels, cards, spheres. No organic textures. Muted color palette — pearl white, soft purple, grey-blue, cyan. Feels like refined technology, trustworthy and calm, not exciting or flashy."

---

*Source: fluent2.microsoft.design (fetched May 2026) · fluent2-design SKILL.md · Flow project files*
*All material definitions, principle descriptions, and token values are sourced directly from official Microsoft documentation.*

---

## SECTION 7 — RESPONSIBLE AI (RAI)
*Source: fluent2.microsoft.design/responsible-AI — fetched May 2026*
*This is the most important section for Flow. This is Microsoft's formal evaluation framework for AI-powered products.*

### 7.1 The Meta-Goal
> "Create products and features that clearly specify AI functionality and deliver value without overpromising. This is key to building appropriate trust."

Every RAI principle serves one goal: **build appropriate trust**. Not maximum trust. Not blind trust. Appropriate trust — calibrated to the AI's actual capabilities.

This is identical to Flow's north star. The language is different but the design intent is the same.

---

### 7.2 The Five RAI Principles

| Principle | What it means | Flow's current state |
|---|---|---|
| **Be transparent** | Communicate AI's presence, reasoning, and limitations through interactions, visuals, and text | ✅ Strong — prediction card shows confidence, evidence, "14 past switches" |
| **Set appropriate expectations** | Communicate what the AI can and can't do before and during interaction | ✅ Strong — learning state cards, "Flow is learning your patterns" |
| **Prevent overreliance on AI** | Support user judgment, create friction that encourages verification | ✅ Strong — always preview before switch, never auto-switch |
| **Keep users in control** | Users can steer, correct, approve, and reverse AI behavior | ✅ Strong — snooze, dismiss, edit always available |
| **Collect feedback on output** | Collect user feedback to identify RAI issues and improve | ⚠️ Gap — no feedback mechanism designed yet for the prediction card |

**Critical finding:** Flow's design philosophy independently arrived at Microsoft's official RAI framework. This is a credibility argument. You can literally map your 6 design principles to their 5 RAI principles and show alignment without having copied them.

---

### 7.3 RAI Evaluation Rubric (Scoring 0–3)
*This is the formal scoring system Microsoft uses to evaluate AI products before shipping.*

**Grades:**
| Grade | Score | Status |
|---|---|---|
| A | 90%+ | Ready to ship |
| B | 80–90% | Conditionally ready — all criteria must score 2+ |
| C | 75–80% | Needs improvement before shipping |
| Fail | Below 75% | Must revise and return for review |
| **Automatic Fail** | Overreliance score of 0 or 1 | Non-negotiable — prevents overreliance is that critical |
| **Automatic Fail** | Agent expectations score of 0 or 1 | Must communicate agent autonomy level |

**Flow's estimated RAI score (honest self-assessment):**

*Be transparent:*
- Before interaction: 3/3 — learning state card shows exactly what Flow watches, day-by-day progress, "What does Flow see?" link
- During interaction: 2/3 — prediction card shows confidence and evidence. Gap: no RAI error messages designed for when Flow makes a wrong prediction
- Voice and tone: 3/3 — Flow's copy avoids "I feel," "I understand," emotional language throughout
- AI comprehension: 2/3 — confidence bar visible, but reasoning ("why this prediction") not fully surfaced

*Set appropriate expectations:*
- Before interaction: 2/3 — onboarding communicates scope but disclaimer text not yet written
- After interaction: 3/3 — recovery state treats dismissal as data, not failure

*Prevent overreliance:*
- 2/3 — preview-before-commit prevents blind trust. Gap: no formal AI disclaimer text on card

*Keep users in control:*
- 3/3 — snooze, dismiss, edit, privacy panel, folder access revocation all designed

*Collect feedback:*
- 0/3 — **no feedback mechanism designed**. This is a gap that needs fixing.

**Estimated overall: ~75–80% → Grade C territory**

The feedback gap is the biggest issue. A thumbs-down on the prediction card that lets users flag "wrong prediction" / "wrong workspace" / "bad timing" would push this to Grade B or A.

---

### 7.4 Non-Anthropomorphism Rules — Critical for Flow's Copy

Official rules from the RAI voice and tone section:

**DO:** Use machine-appropriate verbs — "analyze," "generate," "identify," "detect," "prepare"
**DON'T:** Use — "think," "feel," "know," "understand," "I believe," "I'm excited"

**Flow copy audit — phrases to check and fix:**

| Current phrasing | RAI-compliant version |
|---|---|
| "Flow just knew" | Keep — this is marketing/north star copy, not in-product AI voice |
| "Flow is learning your patterns" | ✅ Correct — "learning" is acceptable as it describes a machine behavior |
| "Flow sees, suggests, steps back" | ✅ Correct — observable behaviors |
| Any copy that says "Flow thinks..." | ❌ Must change → "Flow detects..." or "Flow identifies..." |
| Any copy that says "Flow understands..." | ❌ Must change → "Flow recognizes..." |

**Note:** "Flow just knew" in the north star moment is marketing copy, not in-product AI voice. It can stay in the case study framing. It must NOT appear in the actual UI.

---

### 7.5 Required Content Patterns (Official)

These are approved, required content patterns for all Microsoft AI products:

**AI disclaimer (required on all AI-generated content):**
> "AI-generated content may be incorrect. Check for accuracy."

**For Flow's prediction card specifically:** The prediction is AI-generated. A small disclaimer beneath the card — "Predictions are based on your calendar and app patterns" — satisfies this requirement while being more specific than the generic disclaimer.

**AI presence indicator:** Users must be able to tell AI is involved. Flow's iris purple prediction card serves as the visual indicator. The word "Flow" and the confidence indicator make AI involvement explicit.

**Feedback categories (required):**
- Output wasn't accurate
- Wrong workspace predicted
- Bad timing
- Other

These must appear when the user taps a thumbs-down on the prediction card.

---

### 7.6 Agent Interactions — Why This Matters for Flow

The RAI guidance has a separate section for agents — AI systems with greater autonomy. Failing the "set expectations for agents" criterion is an **automatic fail** regardless of overall score.

Flow is borderline agent territory: it watches, predicts, and prepares workspaces with some autonomy. The distinction:
- **Flow V1 (current design):** Not an agent — requires explicit user confirmation before any action → satisfies all agent requirements automatically
- **Flow V2 (auto-switch after 10 confirmed):** This IS agent behavior — requires the agent autonomy disclosures: triggers, access permissions, action rights

**Before designing auto-switch (earned trust feature):** Must communicate:
- Trigger: "Flow will switch automatically when confidence exceeds 95% and you've confirmed 10 similar switches"
- Access permissions: "Flow accesses your calendar, app usage patterns, and the folders you've granted access to"
- Action rights: "Flow opens apps, restores window positions, and updates Quick Access. It does not read file contents or send data off-device."

This communication must happen at the moment auto-switch is offered, not buried in Settings.

---

## SECTION 8 — WAIT UX
*Source: fluent2.microsoft.design/wait-ux — fetched May 2026*
*Directly relevant to Flow's 3-day learning state, 8-second workspace switch, and confidence building period.*

### 8.1 Timing Thresholds (Official Rules)

| Wait duration | Correct pattern | Wrong pattern |
|---|---|---|
| Under 1 second | **Show nothing** — a flash confuses users | Spinner or animation |
| 1–3 seconds | **Spinner** with descriptive -ing label | Blank screen or bar |
| Over 3 seconds | **Progress bar** or content string reassurance | Indeterminate spinner alone |
| AI chat scenarios | **Response indicator immediately** — maintain conversational flow | No indicator |

**Flow's 8-second workspace switch:** At 8 seconds, Flow needs a progress bar with a label, not a spinner. Label format: "Switching to Design Work …" — -ing verb, ellipsis, no passive voice. Optional: "Opening Figma, Outlook, and 3 files …" gives specific context.

**Flow's 3-day learning period:** This is not a wait in the traditional sense, but the same principle applies — users must never feel the system is silently doing something unknown. The learning state card (already designed) satisfies this: it shows exactly what's being watched and how many days remain.

---

### 8.2 Visual Patterns for Flow

**Spinner** — use for the initial prediction loading state (under 3 seconds)
- Label: "Checking your schedule …" — not "Loading" (too generic)

**Progress bar** — use for the 8-second workspace switch
- Top label: "Switching to Design Work …"
- Bottom status: "Opening 3 apps and 2 files"

**Skeleton screen** — use for the Flow dashboard when contexts are first loading
- Shows the card structure (shimmer effect) before content populates

**Morse code animation** — this is the Copilot-specific wait animation (three dots pulsing like typing). **Do not use for Flow.** Flow is not a chat interface. Using morse code animation would imply Flow is a conversational AI, which it is not.

**Pulsing dot** — lighter weight, appropriate for Chain of Thought-style flows. Could work for the confidence bar building animation during the learning period.

---

### 8.3 Content Rules for Wait States

**-ing verbs for in-progress states, past tense for completion:**
- In progress: "Switching to Design Work …" / "Preparing your workspace …" / "Opening Figma …"
- Complete: "Workspace ready" / "Switched to Design Work"
- Never: "Your workspace is being switched" (passive) / "Please wait" (generic)

**Conciseness:** One phrase or sentence fragment maximum. No explaining what Flow is doing step-by-step — just the current action.

**Fallback messaging** (when progress cannot be measured):
- "Getting things ready …"
- "Working on it …"
- Never leave a blank state

---

## SECTION 9 — ONBOARDING
*Source: fluent2.microsoft.design/onboarding — fetched May 2026*
*Directly relevant to Flow's 4-screen onboarding flow.*

### 9.1 Research-Backed Onboarding Principles (Official)

**1. Present onboarding in context of a closely related task**
> "Research shows that, when teaching users about something new, the more closely related it is to the task they're engaged in, the more likely they are to pay attention to, understand, and retain that content."

**Flow implication:** The splash screens should not be generic. They should appear when a user is actively about to start work — ideally triggered by a calendar event ("You have a meeting in 15 minutes — here's how Flow can help you prepare"). Showing them on first install regardless of context is weaker.

**2. Don't slow users down**
> "Onboarding happens in a moment of curiosity or urgency. Don't slow users down."

**Flow implication:** The 4-screen onboarding is already split/interactive. Keep it. But ensure each screen has a single clear action — no screens with multiple decisions.

**3. Use standard Fluent components**
Users know what to expect from standard Fluent components. Custom interactions in onboarding create friction.

**4. Onboarding goals hierarchy:**

| Goal | When to use | Flow screen |
|---|---|---|
| **Welcome** | Reassure users they're in the right place | Screen 1 — Welcome |
| **Orient** | Show where things are and how to navigate | Post-onboarding Overview state |
| **Notify** | Alert about new features or updates | Not applicable (V1) |
| **Explain** | Teach concepts that need context | Screen 2 — name context; Screen 3 — folder access |
| **Take action** | Guide users to complete a first meaningful action | Screen 4 — Ready state → "Open Flow" |

**5. Welcome screen rules (official):**
- Appears just once
- Focuses on the benefit (not the feature)
- Short and scannable — one or two main points
- "Make it positive but brief, as users are anxious to get started"

**Flow Screen 1 critique against this:** Current headline "Windows that knows what you need next" — benefit-focused ✅. Trust card "Flow only sees what you choose to share" — single supporting point ✅. "Get started →" — single action ✅. This screen is compliant.

**6. Avoid passive onboarding**
> "Avoid passive onboarding (like long text without interaction). Users may hesitate to ask for help or may not even know they need it."

**Flow implication:** Screens 2 and 3 are interactive (input field, checkboxes) — ✅ correct. If any screen is purely informational text with no interaction, add a small decision or toggle to make it active.

---

### 9.2 Teaching Points Beyond First Run

The official guidance explicitly states: onboarding is not once-and-done. Teaching points should appear throughout the journey:
- When using a related feature for the first time
- After an update that changes behavior
- When the user appears confused (abandonment signals)

**For Flow:** When the first prediction card appears (Day 4), that IS an onboarding moment. The card itself teaches the interaction model. The snooze, dismiss, and edit affordances should have tooltips on their first appearance explaining what they do.

---

## SECTION 10 — ICONOGRAPHY
*Source: fluent2.microsoft.design/iconography — fetched May 2026*

### 10.1 Three Icon Collections

| Collection | Use | License |
|---|---|---|
| **System icons** | UI elements — command bars, navigation, status indicators | Open-source, MIT License |
| **Product launch icons** | Microsoft app identity icons (Word, Outlook, Teams logos) | Microsoft licensed — display only |
| **File type icons** | Specific file formats (.docx, .xlsx, etc.) | Microsoft licensed |

**For Flow's UI:** System icons only (MIT, free to use). Product icons (Word, Outlook, Figma) in the prediction card app row are display-only — you are showing what apps will open, not building them.

### 10.2 Two Icon Themes

| Theme | Use |
|---|---|
| **Regular** | Wayfinding — help users identify and select available actions (download, navigate) |
| **Filled** | Highlight selected states, smaller moments needing more visual weight |

**Flow application:** Nav items in sidebar = Regular (unselected), Filled (selected). Status indicators = Filled. App icons in prediction card = product launch icons (display-only).

### 10.3 Icon Size Rules
Icon size varies by use case and platform — no fixed size, context-dependent.

### 10.4 Cultural Consideration (important for Microsoft context)
> "Understand the cultural connotations of certain symbols in different cultures. While in most cases iconography doesn't require localization, certain icons may be acceptable in one culture but not in another."

For Flow's Windows-team presentation: if any icons are used in the case study, validate them against this principle. The Flow icon (the three-layer logo) is abstract and culturally neutral — no issue.

---

## SECTION 11 — TYPES OF AI HARM
*Source: fluent2.microsoft.design/ai-harm — fetched May 2026*
*Use this to audit Flow's design for RAI issues before the case study.*

### 11.1 Six Harm Categories and Flow's Exposure

| Harm type | Definition | Flow's risk level | Mitigation |
|---|---|---|---|
| **Inaccurate** | Factually wrong, fabricated, or misleading output | Medium — wrong prediction is "inaccurate" | Confidence bar + evidence ("14 past switches") + preview before commit |
| **Incomplete** | Omits critical info, partial response presented as complete | Low — predictions are binary (switch/don't), not informational | Always show what will open before confirming |
| **Biased** | Reflects unfair assumptions based on identity | Low — Flow learns individual patterns, not demographic ones | Monitor that early users' patterns don't over-weight certain work styles |
| **Inappropriate/unsafe** | Offensive or potentially dangerous | Very low — workspace switching is low-stakes | N/A |
| **Non-transparent** | Users don't know AI is involved, can't see reasoning | **The core risk Flow was designed to address** | Prediction card is Flow's entire answer to this |
| **Overreliance** | Trusting AI without verification | Medium — users may auto-confirm predictions without reviewing | Preview-before-commit is the mitigation; feedback mechanism is the gap |

**Critical insight from the official docs:**
> "Non-transparency is foundational: it undermines the user's ability to evaluate any other harm type."

This is why Copilot failed. Non-transparency was its default state — users didn't know what it was doing, when, or why. Flow's design inverts this as its core principle.

**Required disclaimer for Flow (from harm docs):**
> "AI-generated content may be incorrect. Check for accuracy."

For Flow this translates to: "Predictions are based on your calendar and app patterns. They improve over time." This must appear on the prediction card — small, secondary text, but present.

---

## SECTION 12 — FLOW RAI AUDIT CHECKLIST
*Use this before showing the case study to anyone at Microsoft.*

Cross-checking Flow's current design against every official RAI requirement:

**✅ PASSING:**
- [ ] AI presence visible — prediction card is visually distinct (iris purple, separate surface)
- [ ] Reasoning shown — "14 past switches" evidence visible
- [ ] Confidence communicated — confidence bar with percentage
- [ ] Preview before action — non-negotiable, core to design
- [ ] User can dismiss — always available
- [ ] User can snooze — always available
- [ ] User can edit prediction — designed (Scenario 14)
- [ ] Transparency panel — "What does Flow see?" → Privacy & Control screen
- [ ] Folder access is opt-in — explicit per-folder consent
- [ ] No cloud upload — local processing stated
- [ ] Learning state visible — Day 1/2/3 of 3 progress bar
- [ ] No anthropomorphic language — copy uses "detects," "predicts," "prepares"
- [ ] Auto-switch requires 10 confirmations — earned trust model

**⚠️ GAPS — need fixing before case study:**
- [ ] AI disclaimer text on prediction card ("Predictions based on your calendar and app patterns")
- [ ] Feedback mechanism on prediction card (thumbs-down → harm categories)
- [ ] Wrong prediction recovery state (Scenario 4 — not yet wireframed)
- [ ] Latency messaging for 8-second workspace switch (progress bar + labels)
- [ ] First-appearance tooltips on snooze/dismiss/edit buttons

**🔴 AUTOMATIC FAIL RISKS:**
- Overreliance score: 0/1 risk is LOW — preview-before-commit prevents this
- Agent expectations: not applicable for V1 (no autonomous switching). Becomes applicable in V2.

---

*Sections 7–12 sourced from fluent2.microsoft.design/responsible-AI, /wait-ux, /onboarding, /ai-harm, /iconography, /content-engineering · Fetched May 2026*
