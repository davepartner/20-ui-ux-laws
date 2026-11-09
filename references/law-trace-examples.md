# Worked "Trace" Examples

The Trace block records *why* a decision was made, mapped to a law. Use these as a style reference
for your own traces. Keep each trace to 2–3 decisions — the point is the strongest drivers, not an
exhaustive list.

---

## 1. Checkout / Payment Flow

```
Trace:
- Decision: Split into "Cart → Shipping → Payment → Review" stepper
  → Law: Hick's Law (one decision set per screen) + Goal-Gradient Effect ("Step 2 of 4" bar)
- Decision: "Pay" button 44px+, sticky at bottom-right, accent color
  → Law: Fitts's Law (large predictable target) + Von Restorff Effect (sole accent)
- Decision: Card number auto-formats into 4-digit chunks; phone strips spaces
  → Law: Postel's Law (forgiving input) + Miller's Law (chunked digits)
```

---

## 2. Pricing Page

```
Trace:
- Decision: Exactly 3 tiers, middle tier highlighted + labeled "Recommended"
  → Law: Paradox of Choice (≤3 options, explicit default) + Von Restorff (accent on the default)
- Decision: Each tier wrapped in a bordered, radiused card with equal internal padding
  → Law: Law of Common Region (containment) + Law of Similarity (same structure = comparable)
- Decision: "Most Popular" badge on the recommended tier
  → Law: Von Restorff Effect (isolates the choice)
```

---

## 3. Global Navigation

```
Trace:
- Decision: Dashboard/Home first, "Log out" / "Delete account" last (far right)
  → Law: Serial Position Effect (edges are remembered) + Fitts's (destructive actions distant)
- Decision: Nav links chunked into groups of 3–5 with dividers
  → Law: Miller's Law (chunking) + Law of Proximity (grouped by gap)
- Decision: Search bar top-right, profile avatar far top-right
  → Law: Jakob's Law (standard placement)
```

---

## 4. Multi-Step Onboarding / Settings

```
Trace:
- Decision: 18-field settings form split into 4 tabbed sections
  → Law: Hick's Law (less choice per screen) + Tesler's Law (complexity absorbed by tabs)
- Decision: "Step 2 of 4" progress indicator with completion bar
  → Law: Goal-Gradient Effect (accelerates completion)
- Decision: Email/name pre-filled from account; timezone derived from browser
  → Law: Parkinson's Law (automate/pre-fill) + Tesler's Law (derive, don't ask)
```

---

## 5. Data Table / Dashboard

```
Trace:
- Decision: Columns aligned to a strict grid; rows with consistent zebra/divider rhythm
  → Law: Law of Continuity (clean axes) + Law of Proximity (row grouping)
- Decision: Status badges use semantic tokens (success/warning/danger) consistently
  → Law: Law of Similarity (same state = same look)
- Decision: Inline skeleton rows while data loads
  → Law: Law of Closure (signal loading) + Doherty Threshold (<400ms perceived)
```

---

## 6. Form with a Destructive Action

```
Trace:
- Decision: "Delete account" placed at the bottom, styled with danger color, behind a confirm
  → Law: Fitts's Law (distant/gated destructive) + Serial Position (terminal action at periphery)
- Decision: Fields grouped into fieldsets with legends of 3–5 fields each
  → Law: Miller's Law (chunking) + Law of Common Region (fieldset containment)
- Decision: Inline validation with error messages that preserve entered data
  → Law: Postel's Law (resilient input) + Doherty Threshold (instant inline feedback)
```

---

## 7. Profile Page & Logout

```
Trace:
- Decision: Profile grouped into Personal info · Security · Preferences · Privacy & data · Danger zone
  → Law: Miller's Law (3–5 chunks) + Law of Common Region (sectioned cards)
- Decision: Logout is the LAST item in the profile dropdown
  → Law: Serial Position Effect (terminal action at the periphery) + Jakob's Law (standard placement)
- Decision: Logout opens a confirmation dialog with a "why are you logging out?" select
  → Law: Fitts's Law (destructive action gated) + Peak-End Rule (a deliberate, safe ending)
- Decision: Reason saved to the DB, then the session invalidated server-side
  → Law: Postel's Law (optional input, never block) + trust/safety (real server-side logout)
```
