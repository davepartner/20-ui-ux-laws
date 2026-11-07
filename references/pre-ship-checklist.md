# Pre-Ship Checklist — The 20 Laws Audit

Run this before delivering any UI. Every item maps to a law. A "no" on any line is a defect.

## Cognitive & Psychological

- [ ] **Hick's Law** — Complex flows are split into wizards/accordions/tabs; no screen exposes >5
      primary actions.
- [ ] **Fitts's Law** — All interactive elements have ≥44×44 px hit targets; primary CTAs sit in
      predictable zones; destructive actions are distant or gated.
- [ ] **Jakob's Law** — Navigation, search, profile, and primary actions follow standard placement
      and platform conventions.
- [ ] **Miller's Law** — Nav links, form fields, and data are chunked into groups of 3–5; phone/card
      numbers are visually chunked.
- [ ] **Aesthetic-Usability** — Strict type scale applied; no raw/unstyled native form controls;
      consistent radii.
- [ ] **Postel's Law** — Forgiving input (auto-strip, masks, trim); backend errors are
      human-readable and preserve user input.
- [ ] **Tesler's Law** — No raw technical complexity leaks to the user; derivable values are derived.
- [ ] **Parkinson's Law** — Known data is pre-filled; sensible defaults and automation present.

## Visual Perception & Gestalt

- [ ] **Proximity** — Label↔input gap is tight; section gaps are clearly larger.
- [ ] **Similarity** — Same-function elements share identical tokens (color, weight, border, radius).
- [ ] **Common Region** — Related modules are wrapped in a bordered/radiused container.
- [ ] **Closure** — Off-screen/loading content signaled via peek-states, scroll fades, or skeletons.
- [ ] **Continuity** — Lists, tables, and steppers aligned on clean vertical/horizontal axes.
- [ ] **Peak-End** — Workflows end with a deliberate, satisfying success state.

## Attention, Performance & Feedback

- [ ] **Serial Position** — Priority items at start; terminal actions at the periphery.
- [ ] **Von Restorff** — Exactly one high-contrast accent marks the primary action.
- [ ] **Occam's Razor** — No redundant wrappers, icon clutter, or decoration.
- [ ] **Doherty Threshold** — Every async operation gives feedback <400ms (optimistic UI, spinner,
      skeleton).
- [ ] **Goal-Gradient** — Multi-step flows show a progress indicator (bar or "Step N of M").
- [ ] **Paradox of Choice** — ≤3 parallel options with a clearly highlighted "Recommended" default.

## Universal Standards

- [ ] All interactive elements have a visible `:focus-visible` state.
- [ ] Text contrast ≥ 4.5:1 (3:1 for large text).
- [ ] `prefers-reduced-motion` is respected.
- [ ] Responsive at small / medium / large breakpoints.
- [ ] Semantic elements + correct `aria-*` attributes throughout.
- [ ] No raw stack traces or leaked technical identifiers in error states.

---

## Usage

1. After implementing, check every box.
2. Fix every "no" before declaring the UI done.
3. Append the `Trace` block (see `law-trace-examples.md`) listing the 2–3 primary laws behind the
   key decisions.

**A UI is only "done" when this checklist passes and the Trace is attached.**
