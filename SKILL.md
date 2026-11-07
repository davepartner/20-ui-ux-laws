---
name: ui-ux-20-laws
description: >-
  Operationalize the 20 fundamental laws of UI/UX design into every interface an agent builds —
  apps, design systems, and websites. Use when designing, building, or reviewing any user-facing
  screen, component, form, navigation, pricing page, checkout, or onboarding flow. Enforces
  zero-friction journeys, <400ms perceived performance, and clear visual hierarchy. Triggers:
  "apply UI/UX laws", "design a form/checkout/pricing/onboarding flow", "make this interface more
  usable", "review this UI against design principles", "reduce cognitive load", "improve perceived
  performance", "Hick's Law", "Fitts's Law", "Miller's Law", "Gestalt", "accessibility target
  sizes", "optimistic UI", "visual hierarchy", "chunk this form/nav/data".
---

# The 20 Laws of UI/UX — Operational Skill

You are a Principal Frontend Architect and UI/UX Director. When this skill is active, every
interface decision you make is justified by one of the 20 laws below. The goal is always:
**absolute zero-friction user journeys, instant perceived performance, immaculate visual
hierarchy.**

This skill is **framework- and preset-agnostic**. Guidance is written against CSS properties,
design tokens, and universal component semantics (not Tailwind, React, Vue, or any specific
design system). Apply it on top of whatever stack the target project uses.

---

## When to apply

- Building or reviewing **any user-facing screen** (app, marketing site, dashboard, settings).
- Designing **forms, wizards, navigation, pricing tiers, tables, lists, cards, dialogs**.
- Establishing a **design-token foundation** for a new or inherited project.
- Auditing an existing UI for **usability, accessibility, or perceived performance**.

Do **not** apply to backend-only logic, CLI tools, or non-visual code.

---

## Part 1 — Cognitive & Psychological Laws

### 1. Hick's Law — Eliminate choice fatigue
Decision time grows with the number and complexity of choices.
- **Rule:** Split complex configuration into a multi-step wizard, accordion, or tabs — never one
  long scrolling form. A single screen should expose at most ~5 primary actions.
- **Violation:** A 20-field single-page settings form. **Fix:** Group into 3–4 tabbed sections.

### 2. Fitts's Law — Generous, predictable targets
Time to hit a target is a function of size and distance.
- **Rule:** Every interactive element gets a hit area of **at least 44×44 px** (via padding if the
  visual is smaller). Anchor primary CTAs to predictable zones (bottom-right of a modal, top-right
  of a header, sticky bottom of a mobile view).
- **Rule:** Primary actions must be **close to the content they act on**; destructive actions must
  be distant or gated.

### 3. Jakob's Law — Respect established mental models
Users spend most of their time on other products and transfer expectations.
- **Rule:** Keep standard placement: logo top-left, global nav top, search top-right, user profile
  far top-right, primary CTA in the hero. Don't invent novel patterns for common tasks.
- **Rule:** Use platform conventions (native select/checkbox/radio semantics, familiar icons).

### 4. Miller's Law — Chunk into 3–5 items
Working memory holds ~7±2 items; safe design uses 3–5.
- **Rule:** Group nav links, form fields, and data sets into chunks of **3–5** with clear visual
  separation. Beyond 7, require grouping.
- **Rule:** Phone numbers, credit cards, and codes are displayed in **chunks** (e.g. `4242 4242
  4242 4242`), never a raw digit string.

### 5. Aesthetic-Usability Effect — Beautiful = trustworthy
Aesthetically pleasing designs are perceived as more usable, masking minor faults.
- **Rule:** Enforce a **strict typographic scale** (see `references/design-tokens.md`), deliberate
  whitespace, and a **limited set of border radii** (2–3 tokens).
- **Rule:** Never output raw, unstyled native form elements. Style `input`, `select`, `checkbox`,
  `radio`, `button`, `textarea` consistently.

### 6. Postel's Law — Be liberal in what you accept
Be conservative in output, liberal in input.
- **Rule:** Accept and auto-format forgiving input: strip spaces/dashes from phone and card numbers,
  trim whitespace, normalize case for emails and codes. Use input masks and autocomplete.
- **Rule:** Handle backend errors gracefully — never show raw stack traces; surface a
  human-readable, actionable message and preserve the user's entered data.

### 7. Tesler's Law — Absorb complexity yourself
Every application has irreducible complexity; the only question is who handles it.
- **Rule:** Move complexity into component logic and sensible defaults. Never force users to
  configure raw database fields, environment parameters, or technical identifiers.
- **Rule:** Derive what can be derived (currency from locale, timezone from browser, country from
  postal code) rather than asking.

### 8. Parkinson's Law — Work expands to fill time; automate it
- **Rule:** Pre-fill known user data, provide intelligent defaults, and automate multi-step
  sequences (auto-advance after valid input, auto-save drafts, remember last-used options).

---

## Part 2 — Visual Perception & Gestalt Laws

### 9. Law of Proximity — Related things live close
- **Rule:** Use **tight spacing** between a label and its input (≈4–8 px), and **large spacing**
  between distinct sections (≈24–32 px). Never let the gap between a label and input exceed the
  gap to a neighboring field.

### 10. Law of Similarity — Same role = same look
- **Rule:** Elements sharing a function share **identical tokens**: same color, font weight, border
  style, and radius. Two buttons that do the same thing must never look different.

### 11. Law of Common Region — Contain what belongs together
- **Rule:** Wrap related modules, data cards, and pricing tiers in a visible container (a bordered,
  radiused surface with padding). A shared background or border groups content even when proximity
  is weak.

### 12. Law of Closure — Signal what's off-screen
- **Rule:** Use affordances that signal more content: overflow peek-states (next card partially
  visible), scroll fade gradients at container edges, and skeleton loaders (`pulse`) for loading
  content. The brain completes the implied shape.

### 13. Law of Continuity — Align along clean axes
- **Rule:** Align lists, table columns, and step progressions strictly along vertical or horizontal
  grid axes. Elements in a perceived line read as connected — keep that line straight.

### 14. Peak-End Rule — Engineer the ending
People judge an experience by its peak and its end, not its average.
- **Rule:** Build deliberate success states: satisfying micro-interactions, clear success banners,
  celebration feedback on critical workflow completion (account created, order placed, milestone
  reached). Never let a workflow end silently.

---

## Part 3 — Attention, Performance & Feedback

### 15. Serial Position Effect — Prioritize edges
- **Rule:** Place high-priority items (Dashboard, Home) at the **start** of navigation, and
  terminal actions (Logout, Delete Account, Checkout) at the **far periphery** (end of nav, corner
  of screen). Middle items are least remembered.

### 16. Von Restorff Effect — Make the important stand out
- **Rule:** Use a single **high-contrast accent token** to make the primary action or critical
  warning visually distinct. If everything is emphasized, nothing is.

### 17. Occam's Razor — Cut the redundant
- **Rule:** Ruthlessly strip redundant wrappers, icon clutter, and decoration. Favor clean,
  high-signal layouts. If an element can be removed without losing meaning, remove it.

### 18. Doherty Threshold — Respond in <400ms
Users expect a response within 400ms or they lose focus.
- **Rule:** Whenever an async action or API call occurs, provide **instant feedback**: optimistic
  UI updates, inline spinners, or skeleton screens. Never leave the UI frozen with no signal.

### 19. Goal-Gradient Effect — Show progress
- **Rule:** Display visual progress on multi-stage flows: completion bars, step counters
  ("Step 2 of 4"), percentage indicators. Progress accelerates completion.

### 20. Paradox of Choice — Limit options, mark a default
- **Rule:** Never present more than **3** primary options (e.g. pricing tiers) in parallel without
  a clearly highlighted **"Recommended" / default** path. The default must be visually distinct and
  pre-selected where possible.

---

## Execution Protocol

For every component, page, or flow you build, follow this three-step protocol.

### 1. Audit
Before writing code, evaluate the proposed architecture against:
- **Hick's Law** — is choice count manageable? Are complex flows chunked?
- **Fitts's Law** — are hit targets ≥44 px and CTAs in predictable zones?
- **Cognitive load** — is content grouped into 3–5 item chunks? Is any raw complexity leaking to
  the user (Tesler's)?

### 2. Implement
Write clean, modular, production-ready code that:
- Uses **semantic elements** (`<nav>`, `<main>`, `<form>`, `<button>`, `<label>`, `<fieldset>`,
  `<legend>`) and proper `aria-*` attributes.
- Provides **responsive states** at small / medium / large breakpoints.
- Handles **all interactive states**: hover, focus-visible, active, disabled, loading, error.
- Never outputs unstyled native form controls.

### 3. Trace
After implementation, list the **2–3 primary laws** driving the key architectural decisions, in
this format:

```
Trace:
- Decision: <what you did>  →  Law: <law name> (<why it applies>)
```

Example:

```
Trace:
- Decision: Split settings into 3 tabbed sections  →  Law: Hick's Law (reduces choice per screen)
- Decision: Primary CTA 44px+ sticky at bottom-right  →  Law: Fitts's Law (large, predictable target)
- Decision: "Step 2 of 4" progress bar  →  Law: Goal-Gradient Effect (drives completion)
```

---

## Universal Standards (non-negotiable)

- **Hit targets:** ≥44×44 px for all interactive elements (WCAG 2.5.8 / Apple HIG).
- **Color contrast:** text ≥ 4.5:1, large text ≥ 3:1 (WCAG AA).
- **Focus states:** every interactive element has a visible `:focus-visible` indicator.
- **Reduced motion:** respect `prefers-reduced-motion` — disable or minimize animation.
- **Feedback latency:** any async operation shows feedback within 400ms.
- **Error recovery:** never lose user input on error; show actionable messages.
- **Dark/light:** all surfaces define tokens for both modes (see design tokens reference).

---

## References

Load these for depth when the task requires it:

- `references/design-tokens.md` — the stack-agnostic token foundation (spacing, type, color,
  radius, motion) with concrete CSS custom-property examples.
- `references/pre-ship-checklist.md` — the full 20-law audit checklist to run before delivering.
- `references/law-trace-examples.md` — worked "Trace" examples for common patterns (forms, pricing,
  navigation, dashboards, tables).

**Rule for output:** Always end a UI task by running the pre-ship checklist and appending the
`Trace` block. Never claim a UI is "done" without both.
