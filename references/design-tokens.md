# Design Token Foundation (Stack-Agnostic)

A shared language so every UI you build is consistent. These are the tokens the 20 laws consume.
Map them onto whatever mechanism your stack uses (CSS custom properties, Tailwind theme, styled
system, Figma variables, etc.).

All values are starting points. The laws constrain the **relationships** more than the exact
numbers — e.g. the gap between a label and its input must be smaller than the gap between sections
(Law of Proximity).

---

## 1. Spacing (Law of Proximity, Law of Continuity)

A tight→loose scale. Use the same token for the same relationship everywhere.

```css
:root {
  /* label ↔ input, icon ↔ label (Proximity: tight) */
  --space-1: 4px;
  /* related elements inside a group */
  --space-2: 8px;
  /* elements within a card / between related controls */
  --space-3: 12px;
  /* card internal padding */
  --space-4: 16px;
  /* between distinct sections (Proximity: loose) */
  --space-6: 24px;
  /* major layout sections */
  --space-8: 32px;
  /* page-level gutters */
  --space-12: 48px;
}
```

**Rule:** the gap between a label and its input (`--space-1` to `--space-2`) must always be
strictly smaller than the gap to the next field or section (`--space-4` to `--space-6`).

---

## 2. Typography (Aesthetic-Usability Effect, Law of Similarity)

A strict modular scale — never ad-hoc font sizes. One scale, applied consistently.

```css
:root {
  --text-xs: 0.75rem;   /* 12px — captions, meta */
  --text-sm: 0.875rem;  /* 14px — secondary text */
  --text-base: 1rem;    /* 16px — body, inputs */
  --text-lg: 1.125rem;  /* 18px — emphasized body */
  --text-xl: 1.25rem;   /* 20px — card titles */
  --text-2xl: 1.5rem;   /* 24px — section titles */
  --text-3xl: 1.875rem; /* 30px — page titles */
  --text-4xl: 2.25rem;  /* 36px — hero */

  --leading-tight: 1.2;   /* headings */
  --leading-normal: 1.5;  /* body */
  --leading-relaxed: 1.75;/* long-form */

  --font-sans: system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
  --font-mono: ui-monospace, "SF Mono", "Menlo", monospace; /* codes, amounts */

  --weight-normal: 400;
  --weight-medium: 500;
  --weight-semibold: 600;
  --weight-bold: 700;
}
```

**Rule:** headings use `--weight-semibold`/`--weight-bold` with `--leading-tight`; body uses
`--weight-normal` with `--leading-normal`. Consistency (Similarity) matters more than the exact
sizes.

---

## 3. Color (Von Restorff Effect, Law of Similarity, Aesthetic-Usability)

Two layers: **neutral surfaces/text** and a small set of **semantic/accent** colors.

```css
:root {
  /* Neutrals — light mode */
  --surface: #ffffff;
  --surface-muted: #f4f4f5;
  --border: #e4e4e7;
  --text: #18181b;
  --text-muted: #71717a;

  /* ONE accent — reserved for the primary action & focus (Von Restorff) */
  --accent: #2563eb;
  --accent-contrast: #ffffff;

  /* Semantic — status only (Similarity: same state = same color) */
  --success: #16a34a;
  --warning: #d97706;
  --danger: #dc2626;
  --info: #0891b2;
}

@media (prefers-color-scheme: dark) {
  :root {
    --surface: #18181b;
    --surface-muted: #27272a;
    --border: #3f3f46;
    --text: #fafafa;
    --text-muted: #a1a1aa;
    --accent: #3b82f6;
  }
}
```

**Rules:**
- **One accent, one job.** Use `--accent` only for the single most-important action per screen and
  for focus rings. If two different elements both scream "click me", neither wins (Von Restorff
  inverted).
- **Status colors only for status.** Success/warning/danger never decorate non-status content.
- **Contrast:** `--text` on `--surface` must be ≥ 4.5:1; large text ≥ 3:1.

---

## 4. Border Radius (Aesthetic-Usability Effect, Law of Similarity)

A **limited set** (2–3 tokens). Consistent corners read as intentional.

```css
:root {
  --radius-sm: 6px;   /* inputs, buttons, small controls */
  --radius-md: 10px;  /* cards, panels, dropdowns */
  --radius-lg: 16px;  /* modals, large surfaces */
  --radius-full: 9999px; /* pills, avatars, toggle knobs */
}
```

**Rule:** same element type → same radius. Inputs are `--radius-sm` everywhere; cards are
`--radius-md` everywhere.

---

## 5. Motion & Timing (Doherty Threshold, Peak-End Rule, reduced-motion)

```css
:root {
  --duration-instant: 100ms;  /* hover, focus, press */
  --duration-fast: 200ms;     /* micro-interactions, toggles */
  --duration-base: 300ms;     /* panel open/close, drawer */
  --ease-out: cubic-bezier(0.22, 1, 0.36, 1);
  --ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);
}
```

**Rules:**
- **All feedback < 400ms** (Doherty). Prefer 150–250 ms for micro-interactions.
- Use `--ease-out` for entrances (settle in), `--ease-in-out` for movement.
- **Celebration** (Peak-End) may exceed the normal budget (300–600 ms) — it is the exception that
  proves the end.

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 6. Elevation & Borders (Law of Common Region)

Use borders and subtle shadows to establish **containers** (Common Region), not decoration.

```css
:root {
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
  --shadow-md: 0 4px 12px rgba(0, 0, 0, 0.08);
  --shadow-lg: 0 12px 32px rgba(0, 0, 0, 0.12);
}
```

**Rule:** a group of related items is wrapped in a surface with `--border` + `--radius-md` +
`--space-4` padding + optional `--shadow-sm`. This is the single pattern for cards, panels, and
pricing tiers.

---

## 7. Layout Grid (Law of Continuity, Law of Proximity)

```css
:root {
  --container-max: 1200px;
  --gutter: clamp(16px, 5vw, 48px);
  --grid-gap: var(--space-6);
}
```

**Rules:**
- Align everything to a consistent column grid (12-col is a safe default) so lists, tables, and
  steppers sit on clean axes.
- Maintain a consistent **left alignment** for labels and a consistent **left alignment** for their
  inputs (never a ragged mix).

---

## Mapping to a specific stack

When you land in a concrete project, translate these tokens 1:1:

| This token | Tailwind (example) | CSS variable (example) |
|------------|--------------------|------------------------|
| `--accent` | `colors.accent` | `var(--accent)` |
| `--radius-md` | `rounded-lg` | `var(--radius-md)` |
| `--space-4` | `p-4` / `gap-4` | `var(--space-4)` |
| `--text-base` | `text-base` | `var(--text-base)` |
| 44 px target | `min-h-11 min-w-11` | `min-height: 44px; min-width: 44px` |

Do **not** paste framework-specific values into the skill. Keep the token layer as the single
source of truth and map at implementation time.
