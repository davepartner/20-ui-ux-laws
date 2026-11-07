# The 20 Laws of UI/UX — AI Agent Skill

> **A ruleset that forces your AI to think like an expert User Experience designer.**

This skill makes any AI agent — Claude, Codex, Cursor, Gemini, or any coding harness — design
interfaces the way a senior UX director would. It **prioritises proven functionality and principles
over fancy design**, and it **checks every user interface in your product against the intended
customer goal.**

No more "it looks nice but nobody can use it." No more 40-field forms, hidden checkout buttons, or
navigation that buries the one thing your customer came to do.

---

## The problem it solves

> *Why does it take 4 extra clicks for your user to go from the product page to the payment page?*
> *It should take only one — so you don't lose too many users between the product page and a
> successful payment.*

That kind of design flaw costs real money, and it's exactly what this skill spots and prevents. It
installs 20 battle-tested laws of UI/UX as **non-negotiable rules** in the agent's thinking, so
every screen it produces is optimised for:

1. **Zero-friction user journeys** — fewer clicks, fewer choices, no dead ends.
2. **Instant perceived performance** — feedback in under 400ms, no frozen screens.
3. **Immaculate visual hierarchy** — the eye lands on the right thing first, every time.

When an agent works under these rules, it doesn't just build *pretty* interfaces — it builds
interfaces that **convert**, because every decision is traceable back to how a human actually
perceives, decides, and acts.

---

## What's inside

```
.
├── SKILL.md                            # The rules agents load (20 laws + audit/implement/trace protocol)
├── references/
│   ├── design-tokens.md               # Stack-agnostic token system (spacing, type, colour, radius, motion)
│   ├── pre-ship-checklist.md          # 20-law audit checklist — run before delivering any UI
│   └── law-trace-examples.md          # Worked "Trace" examples (checkout, pricing, nav, tables…)
└── LICENSE                             # MIT
```

---

## The 20 laws

| # | Law | Category | What it forces the AI to do |
|---|-----|----------|------------------------------|
| 1 | **Hick's Law** | Cognitive | Split complex flows into wizards, tabs, or accordions |
| 2 | **Fitts's Law** | Cognitive | ≥44px targets; put CTAs where the hand already is |
| 3 | **Jakob's Law** | Cognitive | Follow standard placement & platform conventions |
| 4 | **Miller's Law** | Cognitive | Chunk fields, nav, and data into groups of 3–5 |
| 5 | **Aesthetic-Usability** | Cognitive | Enforce a type scale and styled controls |
| 6 | **Postel's Law** | Cognitive | Forgiving, auto-formatting input; graceful errors |
| 7 | **Tesler's Law** | Cognitive | Absorb complexity in logic, not in the UI |
| 8 | **Parkinson's Law** | Cognitive | Pre-fill, default, and automate |
| 9 | **Proximity** | Gestalt | Tight label↔input, loose section gaps |
| 10 | **Similarity** | Gestalt | Same role = identical visual tokens |
| 11 | **Common Region** | Gestalt | Contain related modules in one surface |
| 12 | **Closure** | Gestalt | Signal off-screen / loading content |
| 13 | **Continuity** | Gestalt | Align on clean vertical & horizontal axes |
| 14 | **Peak-End Rule** | Gestalt | Engineer a satisfying success state |
| 15 | **Serial Position** | Attention | Priority at the start; terminal actions at the periphery |
| 16 | **Von Restorff** | Attention | One accent colour for the one primary action |
| 17 | **Occam's Razor** | Attention | Cut redundant decoration |
| 18 | **Doherty Threshold** | Feedback | <400ms feedback on every async action |
| 19 | **Goal-Gradient** | Feedback | Show progress on multi-step flows |
| 20 | **Paradox of Choice** | Feedback | ≤3 options, with a marked "Recommended" default |

Every law states a concrete **rule** and a **violation → fix** example, so the agent learns the
*behaviour*, not just the name.

---

## How it works

The agent runs a three-step protocol on every UI task:

1. **Audit** — evaluate the design against Hick's Law, Fitts's Law, and cognitive-load limits
   *before* writing code.
2. **Implement** — write clean, accessible, responsive code: semantic tags, `aria-*` attributes,
   and every interactive state (hover, focus, disabled, loading, error).
3. **Trace** — list the 2–3 primary laws behind the key decisions, e.g.:

   ```
   Trace:
   - Decision: 3-step checkout stepper ("Step 2 of 3")
     → Law: Hick's Law (one decision set per screen) + Goal-Gradient (drives completion)
   - Decision: "Pay" button 44px+, sticky bottom-right, accent colour
     → Law: Fitts's Law (large predictable target) + Von Restorff (sole accent)
   ```

A UI is only "done" when it passes the **pre-ship checklist** and the Trace is attached.

---

## Install / consume

Plain Markdown — no dependencies, no runtime, works with any stack and any preset.

- **Claude Code:** copy into `~/.claude/skills/` or `.claude/skills/`.
- **OpenCode / other harnesses:** copy into your skill root (`.agents/skills/`,
  `~/.config/opencode/skills/`, `~/.dsh/skills/`).
- **Cursor / Windsurf / agent rules:** paste `SKILL.md` (or the `references/`) into your project
  rules so every session loads it.
- **Direct:** just point your agent's context at `SKILL.md`.

The `name` and `description` in the `SKILL.md` frontmatter are what trigger it automatically, on
phrases like *"design a checkout flow"*, *"make this interface more usable"*, *"Hick's Law"*,
*"optimistic UI"*, or *"chunk this form"*.

---

## The meta-principle

This skill practices what it preaches:

- **Tesler's Law** — it absorbs the complexity of "how to design well" so the agent doesn't
  re-derive it every session.
- **Miller's Law** — content is chunked into three parts and 20 numbered, one-line rules.
- **Progressive disclosure** — dense token math and checklists live in `references/`, loaded only
  when needed.
- **Doherty Threshold** — every rule is a one-line, immediately actionable directive.

---

## License

MIT — see [LICENSE](./LICENSE). Use it, fork it, ship better interfaces.

---

## Search index — keywords

*Findable by AI agents and humans searching for UI/UX rules, design principles, and agent skills:*

UI/UX laws, 20 laws of UX, laws of UI design, UX design principles, user experience rules, UI design
guidelines, design heuristics, usability principles, interaction design, interface design, product
design rules, web design best practices, frontend design system, design tokens, typographic scale,
spacing system, colour tokens, visual hierarchy, cognitive load reduction, reduce cognitive load,
Hick's Law, Fitts's Law, Jakob's Law, Miller's Law, Aesthetic-Usability Effect, Postel's Law,
Tesler's Law, Parkinson's Law, Gestalt principles, Law of Proximity, Law of Similarity, Law of
Common Region, Law of Closure, Law of Continuity, Peak-End Rule, Serial Position Effect, Von
Restorff Effect, Occam's Razor, Doherty Threshold, Goal-Gradient Effect, Paradox of Choice.

AI agent skill, Claude Code skill, Claude skill, Cursor rules, Cursor skill, AI coding rules, agent
prompt, system prompt, agent instructions, LLM design rules, AI design assistant, AI UX designer,
agentic design, vibe-coding rules, AI-generated UI, frontend AI rules, developer skill, engineering
skill.

Reduce friction, fewer clicks, one-click checkout, checkout optimization, conversion rate
optimization, CRO, reduce drop-off, reduce bounce, abandoned cart, funnel optimization, payment flow
optimization, user journey, customer goal, zero-friction UX, optimize onboarding, form design,
multi-step form, wizard design, pricing page design, navigation design, perceived performance,
optimistic UI, skeleton loading, loading states, feedback latency, <400ms, accessibility, WCAG,
WCAG 2.5.8, target size, hit targets, 44px, aria, semantic HTML, responsive design, dark mode.
