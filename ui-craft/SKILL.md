---
name: "ui-craft"
description: "The one design authority for all UI work: screens, components, pages, design systems, restyles and UI reviews in any framework. Brand-specific identity, token-based spacing, type, color and contrast, every state, purposeful motion, and scripted quality gates."
---

# UI Craft

UI that looks like a senior design engineer made it for **this** brand: specific in
identity, strict in its system, accessible by default, and calm in motion.

Five layers, always in this order. A later layer never overrides an earlier one:

1. **Brand direction:** who this is for and what makes it unmistakably theirs.
2. **Tokens:** spacing, sizing, radius, elevation, type, color and motion as named values.
3. **Components and states:** built only from tokens, with every state handled.
4. **Motion:** only where it gives feedback, continuity or hierarchy.
5. **Gates:** anti-slop, accessibility, lint and contrast scripts, visual QA.

## Non-negotiables

- **No design from vibe memory.** Every major choice traces to the brand brief, a
  reference, an existing design system, or a rule in this skill. If it traces to nothing,
  cut it.
- **An existing design system wins.** If the user, org or repo already has tokens, a
  design system artifact or a brand guide, use it and extend it. Never fork it silently.
- **Tokens before code.** No raw hex, px or ms in components. Every value comes from a
  token, and every token has a role.
- **A token's role is part of the token.** A CTA-only accent never becomes a background.
  A status color never becomes decoration.
- **Light mode by default.** Use dark only when the brief asks for it or the brand needs it.
- **Accessibility is built in, not added at the end.** WCAG 2.2 AA is the floor (§8).
- **Every state exists:** default, hover, focus-visible, active, disabled, loading, empty,
  error, success. Also long content, no content, and slow network.
- **Motion has a job, or it doesn't exist.**
- **Spend boldness in one place.** One memorable signature per surface. Everything around
  it is quiet and disciplined.
- **Verify by rendering.** Check the real result at 320, 768, 1024 and 1440 px before
  handoff. Reading the code is not enough.

## Workflow

Pick the lightest path that fits:

- **Small fix or edit to an existing system:** read the existing tokens → apply §3–§7 →
  run the gates in §10.
- **New screen or component in an existing product:** read the existing system → state
  the job of the screen and its states → build → gates.
- **New product, brand direction, redesign or landing page:** do the full flow. Brand
  brief (§1) → research (§2) → tokens (§3–§6) → plan review → build → gates. When several
  directions are plausible, show **three** distinct, reference-locked directions and let
  the user choose before you build.

---

## 1. Brand direction: make it theirs

Write this brief before any visual decision. Ask only for what is missing *and* would
change the result. Otherwise propose your best assumptions and say what they are.

```text
Subject:      what the product is, in the user's own words
Audience:     who uses it, their expertise, and the context they use it in
Job:          the one thing the main screen must make easy
Feel:         3 adjectives it must feel like, and 2 it must NOT feel like
World:        materials, places, culture, vernacular and artifacts from the subject's world
Signature:    the one memorable move (layout, type treatment, interaction, motif or media)
Constraints:  existing brand/design system, framework, platforms, deadline, content
```

**Where identity comes from.** Distinctive choices come from the subject's world, not from
UI trends. For each token family, ask what the world suggests:

| Token family | What to draw it from |
|---|---|
| Palette | the subject's real materials, places and light (stone, paper, signage, landscape, products) |
| Type | the subject's printed or written culture: technical, editorial, civic, craft, luxury |
| Shape (radius) | the subject's objects: machined and sharp, or soft and handmade |
| Density | the user's job: scanning data (dense) or reading and deciding (airy) |
| Motion personality | the brand's tempo: crisp and instant (tools) or soft and slower (lifestyle) |
| Imagery | real photos or screenshots of the subject; never generic blobs or 3D shapes |

**Identity tests.** Run these on the plan *and* on the build:
- *Swap test:* put a coffee shop's or a bank's logo on it. If it still looks plausible,
  the design is generic. Add the detail that makes it this brand's.
- *Nav test:* hide the logo and nav. Is the brand still recognisable?
- *Default test:* if you would have produced the same plan for a similar brief, revise the
  part that came out the same. Say what you changed and why.

## 2. Research and lock the direction

- **Sources, in order of strength:** the user's own references or design system → the
  Refero MCP, if connected (styles for look, screens for patterns, flows for journeys) →
  real products in the same domain → the craft rules in this skill.
- Study 3–4 strong references. **Choose one primary direction.** Borrow 1–2 narrow details
  from the others. **Never average** them into a safe middle: a dark reference doesn't
  become cream, an acid accent doesn't become muted clay, a sharp UI doesn't become soft
  rounded cards.
- Write a reference lock before building:

```text
Primary direction: [one dominant source or idea]
Preserve:          [3–5 traits that must survive: canvas, type, accent, layout, density, media]
Borrow only:       [1–2 specific details from secondary sources]
Role rules:        [which token is for what, e.g. "accent = primary CTA + focus only"]
Media strategy:    [real / generated / screenshot / code-native / honest placeholder + aspect ratio]
Reject:            [defaults that would collapse this direction]
```

- Then write a **decision ledger**: one row per major choice, as
  `| Decision | Source | Role | Why |`. A choice with no source is not shipped.

---

## 3. Spacing and sizing

**Base unit: 4px.** Every margin, padding, gap and size is on this scale. Nothing else.

```css
--space-0: 0;     --space-1: 4px;   --space-2: 8px;   --space-3: 12px;
--space-4: 16px;  --space-5: 20px;  --space-6: 24px;  --space-8: 32px;
--space-10: 40px; --space-12: 48px; --space-16: 64px; --space-20: 80px;
--space-24: 96px; --space-32: 128px;
/* 2px is allowed only for optical nudges, hairlines and focus offsets */
```

**Proximity is hierarchy.** Space inside a group is always smaller than space between groups.

| Relationship | Space |
|---|---|
| Icon ↔ its label; label ↔ its input | 4–8px |
| Items inside one component | 8–12px |
| Related components in a group | 16–24px |
| Separate groups or blocks | 32–48px |
| Page sections | 64–128px (marketing); 32–48px (product UI) |

- Padding inside a container is ≤ the gap that separates it from its siblings.
- **Vertical rhythm:** the spacing step around text is at least half the line-height
  (16px/1.5 → 24px line → 12/24/48 rhythm).
- Fix spacing before you touch fonts. Spacing is what makes two products with the same font
  look different.

**Sizing tokens**

| Element | Size |
|---|---|
| Control height (button, input, select) | sm 32px · md 40px · lg 48px (one height per row) |
| Hit target | ≥ 24×24px (AA floor); 44×44px on touch; 32×32px minimum on desktop for icon buttons |
| Icons | 16px (inline, dense) · 20px (buttons, inputs) · 24px (nav) · 32px+ (empty states) |
| Icon ↔ text pairing | 14–16px text → 16px icon; 16–18px → 18–20px; headings → 20–24px |
| Content measure | prose 60–75ch (max 80); UI descriptions ≤ 45ch |
| Layout | 4/8/12-column grid; container max 1200–1440px; side gutters 16px (mobile) → 24–48px |

**Radius hierarchy.** It comes from the brand's shape language (§1). Never use one radius
for everything.

```css
--radius-none: 0; --radius-sm: 4px; --radius-md: 8px; --radius-lg: 12px; --radius-full: 9999px;
```

- Small controls take smaller radii than the panels that contain them.
- **Nested corners:** inner radius = outer radius − padding (it never goes below 0).
- Pill shapes (`full`) only for chips, toggles and avatars. Never for cards or panels.

**Elevation: 3 levels at most.** It must mean something (resting, raised, overlay).

```css
--shadow-1: 0 1px 2px rgb(var(--shadow-rgb) / 0.06);                                       /* raised controls */
--shadow-2: 0 4px 12px rgb(var(--shadow-rgb) / 0.08), 0 1px 3px rgb(var(--shadow-rgb) / 0.06); /* popovers */
--shadow-3: 0 16px 40px rgb(var(--shadow-rgb) / 0.12), 0 4px 12px rgb(var(--shadow-rgb) / 0.08); /* modals */
```

Tint `--shadow-rgb` toward the brand's darkest neutral, not pure black. In dark mode,
show elevation with lighter surfaces and hairline borders, not shadows.

**Cards are for interaction.** A card is justified only when the container itself is
clickable, a form, or expandable. *Card test:* remove the border, shadow, background and
radius. If nothing about interaction or understanding gets worse, it isn't a card; use
spacing, dividers or columns instead.

## 4. Typography

- **Families:** one is the default; two need a reason (a display face that carries the
  brand, or mono for code and data). Never three. Choose them from the brand's world (§1),
  never as a reflex: a neutral workhorse (Inter, system-ui) is fine for dense product UI
  *only* when the brand's personality is carried somewhere else.
- **Scale:** pick one ratio. 1.125–1.2 for product UI, 1.25–1.333 for marketing and
  editorial. **6–8 sizes in total.** Body text is ≥ 16px; 11px is the absolute floor and
  only for captions.
- **Weights:** 3, at most 4. 400 body · 500 labels · 600 buttons and subheads · 700
  headlines only. Never bold a whole paragraph. Light (300) only at 24px and up.
- **Line-height falls as size grows:** body 1.5–1.7 · UI text 1.3–1.4 · headings 1.1–1.2
  · display 0.95–1.1 · single-line buttons 1. Longer lines need more leading.
- **Tracking (in `em`, size-specific, never one value for everything):**

| Text | letter-spacing |
|---|---|
| Body 14–18px | 0 |
| Small 11–13px; UI labels and buttons | +0.01 to +0.03em |
| ALL CAPS (rare) | +0.06 to +0.10em, always |
| Headings 32px+ | 0 to −0.02em |
| Display 48px+ | −0.02 to −0.03em |

- **Text colors: 3–4 levels** (primary, secondary, tertiary, disabled). Create breathing room
  with space, never by fading text. Secondary text still passes 4.5:1.
- **Hierarchy comes from size + weight + color + space together.** *Squint test:* you can
  see 3 clear levels.
- **Fluid headings:** `clamp(min, rem + vw, max)`. Never `vw` alone, because it breaks zoom.
- **Respect the user's text-size setting:** spacing around text in `rem`/`em`. The layout
  survives 200% zoom.
- **Polish (required):**
  - `text-wrap: balance` on headings and card titles; `text-wrap: pretty` on lead text.
    Check for one-word last lines anyway.
  - `font-variant-numeric: tabular-nums` on tables, prices, stats, timers and counters.
  - Curly quotes and apostrophes (“ ” ’) in copy; `…` not `...`; non-breaking space between
    a number and its unit (`10 MB`).
  - `text-underline-offset: 0.2em` on links; links are distinguishable by more than color.
  - Tabs: reserve the bold width so selecting a tab doesn't shift the row.
  - Buttons and labels: `text-box: trim-both cap alphabetic` for optical centring; then
    re-check the padding.
  - Acronyms in body text: `font-variant-caps: all-small-caps`.
  - Overflow: truncate or clamp with a `title` or tooltip; flex children need `min-width: 0`;
    file names keep their extension visible.
  - `hyphens: auto` in narrow columns, with `lang` set on the html element.
  - Fonts: `font-display: swap`, ≤ 3 weights loaded, variable fonts preferred, the critical
    face preloaded.

## 5. Color and contrast

**Structure: 4 layers, not 30 colors.**

1. **Neutrals: 70–90% of the UI.** An 11-step scale (50–950) carrying a slight tint of the
   brand's hue, warm or cool. Not a stock gray, and not a reflex `#111`.
2. **One primary accent** with a full scale. Default 500–600 · hover +1 step · active +2
   steps · tint 50–100. It is used sparingly, for the primary action, focus, selection and
   key data.
3. **Semantics:** success, warning, danger, info. Each is a set:
   `--x`, `--x-bg`, `--x-border`, `--on-x`. Semantic hues must not collide with the
   primary (blue primary → info uses another treatment).
4. **Effects** (gradients, glows): rare, local, and never the only thing that makes
   something visible.

**Distribution:** 60–80% neutrals · 10–20% text levels · 5–10% accent and semantics. At most
2 colors per component. A hover state is a step on the same scale, never a new hue.

**Naming:** by purpose, never by hue (`--primary`, `--surface-2`, `--text-muted`, `--border`;
never `--blue`). Build scales in **OKLCH** so the steps look even; ship them as hex or OKLCH.

```css
:root {
  --bg; --surface-1; --surface-2; --surface-3;          /* surfaces */
  --text; --text-muted; --text-subtle; --text-disabled; /* text levels */
  --border; --border-strong; --focus-ring;              /* lines */
  --primary; --primary-hover; --primary-active; --primary-tint; --on-primary;
  --success; --success-bg; --warning; --warning-bg; --danger; --danger-bg; --info; --info-bg;
}
```

**Contrast floor (WCAG 2.2 AA). Never round a failing ratio up.**

| Pair | Minimum |
|---|---|
| Body text (< 24px regular, < 18.67px bold) | **4.5:1** |
| Large text | **3:1** |
| Input borders, icons that carry meaning, focus ring, chart marks | **3:1** against what's next to them |
| Text on tinted, translucent or gradient backgrounds | 4.5:1 at the *worst* point |
| Disabled controls | exempt, but still recognisable as disabled |

- Color is never the only signal. Status also gets an icon, text, a pattern or a shape.
- Check every text and surface pair with the contrast script (§10) in light **and** dark.

**Dark theme (only when chosen):** a separate neutral scale, never an inversion. Base
around `#0f0f0f`–`#1a1a1a` tinted with the brand hue (never `#000`); text around
`#f0f0f0` (never `#fff`); raised surfaces are lighter; borders `rgb(255 255 255 / 0.08–0.15)`;
desaturate the accents slightly. Set `color-scheme` on `:root` and a `theme-color` meta tag
for each scheme. Ease the switch between themes; don't flash.

**Also honor** `prefers-contrast: more` (solid backgrounds, defined borders) and
`prefers-reduced-transparency: reduce` (no blur, opaque surfaces).

## 6. Components and states

**Architecture:** small, focused components (split anything over 200 lines). Prefer
composition over configuration. Keep data and container logic separate from presentation.
Styles come only from tokens. A component behaves the same everywhere it appears.

**Every interactive component specifies:**

| State | Rule |
|---|---|
| Hover | one scale step, gated by `@media (hover: hover) and (pointer: fine)` |
| Focus | `:focus-visible` ring: 2px, 3:1 contrast, 2px offset. Never a bare `outline: none` |
| Active / pressed | `scale(0.97–0.98)`, feedback on pointer-**down** |
| Disabled | lower emphasis plus `disabled` or `aria-disabled`; explain why nearby if it isn't obvious |
| Loading | keep the label and width, add a spinner or "Saving…"; block double submits |
| Empty | what goes here + the one action that fills it. Never a blank area |
| Error | what happened + how to fix it, next to the cause; announced to screen readers |
| Success | confirm with the same verb the action used ("Publish" → "Published") |

**Specific components:**
- **Buttons:** one primary per view. Label = verb + object ("Save changes", never "Submit"
  or "OK"). Use a real button element for actions and a link for navigation, never a
  clickable div.
- **Forms:** a visible label on every input (placeholders are examples, not labels).
  Correct `type`, `inputmode` and `autocomplete`. Never block paste. Validate inline after
  blur. On submit, focus the first error and summarize the errors. Mark required fields with
  more than color. Warn before losing unsaved changes. Turn spellcheck off for codes, emails
  and usernames.
- **Popovers, menus and dropdowns:** scale in from the trigger (`transform-origin` at the
  trigger). They close on Escape and on an outside click, and return focus to the trigger.
- **Modals:** for decisions that need focus, not for content that fits inline. Centred
  origin, focus trapped, Escape closes, focus returns, the background is inert,
  `overscroll-behavior: contain`. Ask for confirmation only for destructive, irreversible
  actions; offer undo for everything else.
- **Tooltips:** a short delay on the first one; adjacent ones open instantly with no
  animation. Never put essential information only in a tooltip.
- **Toasts and live updates:** `role="status"` (polite) or `role="alert"` (errors). Pause
  timers on hover and when the tab is hidden. Enter and exit on the same edge.
- **Tabs, listboxes, comboboxes and dialogs:** follow the WAI-ARIA APG pattern exactly.
  In Angular, use the CDK (`a11y`: FocusTrap, LiveAnnouncer, FocusMonitor, ListKeyManager).
- **Loading content:** skeletons shaped like the real content for anything over ~300ms;
  optimistic updates where the action is reversible. Streamed content appears progressively
  and never makes the layout jump.
- **Images and media:** always set `width`/`height` or `aspect-ratio`; `loading="lazy"`
  below the fold; meaningful `alt` (or an empty alt when decorative). Never fake photos or
  illustrations with CSS shapes. Use an honest, sized placeholder with an art-direction note.
- **Icons:** one library and one style (outline *or* solid) across the product.
  `currentColor`. `aria-hidden="true"` when decorative; `aria-label` on icon-only buttons.
  Match the stroke weight to the text weight. Never emoji as icons.
- **Lists of 50+ items:** virtualize them (or use `content-visibility: auto`).
- **URL reflects state:** filters, tabs and pagination live in the URL, so back, share and
  bookmark all work.
- **Wayfinding:** every screen answers "where am I, where can I go, how do I get out".

## 7. Motion

**Purpose first.** Every animation is one of:
- *feedback* (I pressed it, it worked);
- *continuity* (where this came from and went);
- *hierarchy* (look here);
- *preventing a jarring change*.

"It looks cool" is not a purpose on anything users see often.

**Frequency decides whether it animates:**

| How often users see it | Decision |
|---|---|
| 100+ times a day (keyboard shortcuts, command palette, typing) | **No animation.** Never animate keyboard-initiated actions |
| Tens of times a day (hover, list navigation) | Minimal or none |
| Occasional (modals, drawers, toasts) | Standard |
| Rare (onboarding, first success) | Room for one moment of delight |

**Tokens.** Ease and duration follow the brand's tempo (§1): crisp brands sit at the low end.

```css
--ease-out:    cubic-bezier(0.23, 1, 0.32, 1);    /* enter, exit, most UI */
--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);   /* moving or morphing on screen */
--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);    /* sheets, drawers */
--dur-instant: 100ms;  /* press, hover, toggle */
--dur-fast:    150ms;  /* tooltips, small popovers */
--dur-base:    200ms;  /* dropdowns, tabs, accordions */
--dur-slow:    300ms;  /* modals, drawers (up to 500ms for large sheets) */
--dist-sm: 4px; --dist-md: 8px; --dist-lg: 16px;
```

**Rules:**
- Easing: `ease-out` for enter and exit, `ease-in-out` for on-screen movement, `linear`
  only for constant motion (progress bars, marquees). **Never `ease-in` on UI**, because it
  delays the moment the user is watching. Never the weak built-in curves.
- UI animations stay **under 300ms**. Modals, drawers, sheets and toasts are the only
  exceptions (≤ 500ms). **Exit is faster than enter.**
- **Animate only `transform` and `opacity`** (and `clip-path` or `filter` sparingly). Never
  `width`, `height`, `top`, `margin` or `padding`. **Never `transition: all`**; name the
  properties.
- **Never animate from `scale(0)`.** Start from `scale(0.95)` with `opacity: 0`.
- **Origin-aware:** popovers scale from their trigger; modals from the centre. Enter and
  exit along the **same path**.
- **Interruptible:** use CSS transitions (not keyframes) for UI that can be triggered
  rapidly. Never lock input during a transition. Gesture-driven motion uses **springs**
  that start from the current on-screen value and inherit the release velocity.
- **Springs:** default critically damped (no bounce). Add bounce (≈ 0.1–0.2) only when the
  gesture itself carried momentum (a flick or a drag release). Settle fast, with no jello.
- **Gestures:** track 1:1 with pointer capture and respect the grab offset. Dismiss on
  velocity (≈ 0.11 px/ms), not only on distance. Rubber-band at boundaries instead of a
  hard stop. Use ~10px of hysteresis before committing to a direction.
- **Stagger:** 30–80ms between items, one entrance per container. Never block interaction
  while it plays.
- **Page load:** at most one orchestrated moment. Fade-and-slide on every section and hover
  lifts on every card read as generated.
- `@starting-style` for entry transitions where supported. A crossfade that looks off gets
  `filter: blur(2px)` during the swap (keep blur ≤ 20px).
- **Reduced motion is required.** `prefers-reduced-motion: reduce` → replace movement with
  short opacity or color fades (≤ 150ms). Remove parallax, springs, loops and auto-play.
  Keep the feedback, lose the movement. In Angular, check
  `matchMedia('(prefers-reduced-motion: reduce)')` before triggering animations.
- **Debug** at 2–5× slow motion or frame by frame (DevTools Animations panel), then review
  with fresh eyes the next day.

## 8. Accessibility floor (WCAG 2.2 AA)

- Semantic HTML first (button, a, nav, main, label, table with `th scope`).
  ARIA only to fill gaps. `tabindex` > 0 never.
- The whole flow works by keyboard. Focus order follows the visual order. No traps, except
  modals, which trap and then release. A skip-to-content link. Focus moves sensibly after a
  route change or a dialog closes.
- One `h1` per page; heading levels don't skip.
- Contrast as in §5. Targets as in §3. Content reflows at 320px and at 200% zoom with no
  horizontal scroll.
- Async changes are announced (`aria-live` / `role="status"` / `role="alert"`).
  `aria-busy` while loading.
- `lang` on the html element and a descriptive page title. Never `user-scalable=no` or
  `maximum-scale=1`.
- Nothing flashes more than 3 times a second. Auto-playing media has controls.
- Check with axe or Lighthouse where the project allows, plus one keyboard-only pass.

## 9. Copy inside the UI

- **Order:** clarity → respect → character. Name things the way the user thinks, not the
  way the system is built ("notifications", not "webhook config").
- Sentence case. Active voice. Facts over adjectives ("in 10 seconds", not "fast").
- **Product surfaces:** orientation + status + action. Headings describe ("Revenue this
  month"), they don't inspire.
- **Errors:** what happened + what to do next. No apologies, never vague.
- **Empty states:** what will appear here + one action.
- **Real content always.** Lorem ipsum hides wrapping and overflow problems.
- **Cut:** hype (seamless, revolutionary, cutting-edge, powerful, robust), filler (just,
  simply, really), corporate words (leverage, empower, unlock, synergy) and AI-slop
  openers ("In today's fast-paced world", "Supercharge", "Elevate", "Say goodbye to").
  If deleting 30% of the copy makes it better, keep deleting.

---

## 10. Gates: run before every handoff

### A. Anti-slop check

The common fingerprints of generated UI. Each one is allowed **only** with a written reason
from the brief or a reference:

- [ ] Indigo or violet accent (`#6366f1`, `#8b5cf6`, `#7c3aed` and similar)
- [ ] Cream canvas (~`#F4F1EA`) + serif display + terracotta or clay accent ("calm editorial on autopilot")
- [ ] Near-black canvas + one acid green or vermilion accent
- [ ] Identical rounded cards with the same soft shadow; one radius on everything; gradient washes
- [ ] One word in a headline swapped into italic, serif or color
- [ ] A tracked-out ALL-CAPS eyebrow above every heading; `A · B · C` meta strings; `→` on every link
- [ ] `01 / 02 / 03` numbering on content that isn't a sequence
- [ ] A decorative left accent stripe that doesn't mean status, selection or priority
- [ ] Emoji as icons; abstract blobs or generic 3D in place of real media
- [ ] Hero = big number + small label + gradient; left text / right image; hero → features grid → pricing → FAQ → CTA by reflex
- [ ] Dark mode the brief didn't ask for
- [ ] Strong reference traits averaged away; a token used outside its role

Then the identity tests from §1 (swap, nav, default) must pass.

### B. System check

- [ ] Every value comes from a token (no raw hex, px or ms in components)
- [ ] ≤ 8 font sizes · ≤ 4 weights · ≤ 4 text colors · 1 primary accent · ≤ 3 elevations
- [ ] Spacing on the 4px scale; inside-group space < between-group space
- [ ] Radius hierarchy and nested corners are correct; cards only where there's interaction
- [ ] All states in §6 exist; long, empty and error content render well
- [ ] Responsive at 320 / 768 / 1024 / 1440 px; no layout shift on load or when streaming

### C. Scripts

Write these two files once to `scripts/` in the project (or a temp folder), then run them.

**`contrast.py`** checks WCAG ratios for token pairs:

```python
#!/usr/bin/env python3
"""Usage: python contrast.py "#1a1a1a:#ffffff:text" "#8a8a8a:#ffffff:ui" ...
kind = text (4.5), large (3.0) or ui (3.0). Exit code 1 if any pair fails."""
import sys

def lum(h):
    h = h.lstrip("#")
    if len(h) == 3:
        h = "".join(c * 2 for c in h)
    rgb = [int(h[i:i + 2], 16) / 255 for i in (0, 2, 4)]
    lin = [c / 12.92 if c <= 0.04045 else ((c + 0.055) / 1.055) ** 2.4 for c in rgb]
    return 0.2126 * lin[0] + 0.7152 * lin[1] + 0.0722 * lin[2]

def ratio(a, b):
    la, lb = sorted((lum(a), lum(b)), reverse=True)
    return (la + 0.05) / (lb + 0.05)

NEED = {"text": 4.5, "large": 3.0, "ui": 3.0}
failed = False
for arg in sys.argv[1:]:
    fg, bg, kind = (arg.split(":") + ["text"])[:3]
    r = ratio(fg, bg)
    ok = r >= NEED[kind]  # no rounding up
    failed |= not ok
    print(f"{'PASS' if ok else 'FAIL'}  {fg} on {bg}  {r:.2f}:1  (needs {NEED[kind]}:1, {kind})")
sys.exit(1 if failed else 0)
```

**`lint_ui.py`** flags rule breaks in styles and templates:

```python
#!/usr/bin/env python3
"""Usage: python lint_ui.py src/   Scans .css .scss .less .html .ts .tsx .jsx .vue files."""
import pathlib, re, sys

RULES = [
    (r"transition\s*:\s*all\b", "transition: all - name the properties"),
    (r"scale\(\s*0\s*\)", "animating from scale(0) - start at scale(0.95) + opacity 0"),
    (r"\bease-in\b(?!-out)", "ease-in on UI - use ease-out"),
    (r"outline\s*:\s*(none|0)\b", "outline removed - confirm a :focus-visible replacement exists"),
    (r"user-scalable\s*=\s*no|maximum-scale\s*=\s*1\b", "zoom disabled - accessibility violation"),
    (r"#(6366f1|818cf8|4f46e5|8b5cf6|7c3aed|a78bfa|6d28d9)\b", "indigo/violet - needs a brand reason"),
    (r"(?<![\w-])#000(000)?\b(?!\w)", "pure black - use the darkest brand-tinted neutral"),
    (r"<div[^>]*\(click\)|<div[^>]*onClick", "clickable div - use a button or link"),
    (r"tabindex\s*=\s*\"?[1-9]", "positive tabindex - breaks the focus order"),
    (r"\.\.\.(?=[\"'<])", "three dots in copy - use the … character"),
    (r"letter-spacing\s*:\s*-?[\d.]+px", "letter-spacing in px - use em"),
]
OFF_SCALE = re.compile(r"\b(margin|padding|gap|inset|top|right|bottom|left)[\w-]*\s*:\s*([^;}{]+)")
PX = re.compile(r"(\d+(?:\.\d+)?)px")
EXT = {".css", ".scss", ".less", ".html", ".ts", ".tsx", ".jsx", ".vue"}

def scan(path):
    issues = 0
    for f in pathlib.Path(path).rglob("*"):
        if f.suffix not in EXT or "node_modules" in f.parts or not f.is_file():
            continue
        for n, line in enumerate(f.read_text(errors="ignore").splitlines(), 1):
            for pat, msg in RULES:
                if re.search(pat, line):
                    print(f"{f}:{n}: {msg}"); issues += 1
            m = OFF_SCALE.search(line)
            if m:
                for v in PX.findall(m.group(2)):
                    if float(v) % 4 and float(v) not in (1, 2):
                        print(f"{f}:{n}: {v}px off the 4px spacing scale - use a --space token"); issues += 1
    return issues

total = sum(scan(p) for p in (sys.argv[1:] or ["."]))
print(f"\n{total} issue(s)")
sys.exit(1 if total else 0)
```

Each lint hit is a prompt to check, not an automatic failure: fix it, or write down why it
is intended.

### D. Visual QA (render it)

Screenshot the real build at 320 / 768 / 1024 / 1440 px, in light (and dark, if it exists),
with hover, focus, loading, empty and error states shown. Compare against the reference
lock. Rate each issue:
- **P0:** broken, unreadable, or a severe accessibility failure
- **P1:** major drift from the direction, or a usability regression
- **P2:** a missing state, a responsive issue, moderate drift
- **P3:** polish

Never hand off with an open P0–P2 unless it's blocked; say what blocks it.

## Review format

When reviewing UI code, report findings as one table, most severe first:

| Sev | Before | After | Why |
|---|---|---|---|
| P1 | `transition: all 300ms` | `transition: transform 200ms var(--ease-out)` | Name the properties; under 300ms |
| P2 | `color: #9ca3af` on `#fff` (2.5:1) | `var(--text-muted)` (4.8:1) | Secondary text must pass 4.5:1 |