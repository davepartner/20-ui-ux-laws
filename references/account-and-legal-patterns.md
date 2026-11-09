# Account & Auth Surfaces — World-Standard Rules

Every authenticated product has the same handful of high-risk surfaces: the **profile page**, the
**logout flow**, and the **legal & support pages**. Getting them wrong causes account takeover, GDPR
breaches, and users who can't leave. These rules operationalize the 20 laws for those surfaces.

Applies to any web app or mobile app that has accounts.

---

## 1. Profile page

### Structure (top → bottom)

1. **Identity header** — avatar (with initials fallback), display name, email/username, role badge,
   "member since". One clear **Edit profile** action (or inline editing with save/cancel).
2. **Grouped sections** — chunk into 3–5 (Miller's Law):
   - **Personal information** — name, email, phone (collect only what you need).
   - **Security** — password change, two-factor authentication, active sessions/devices, email
     verification status.
   - **Preferences** — language, timezone, theme, notifications.
   - **Privacy & data** — visibility, data export, connected accounts.
   - **Danger zone** — deactivate / delete account, visually separated at the bottom.

### Rules

- **Avatar** — accept common image types with a size limit, crop to 1:1, and always provide an
  initials/identicon fallback. Store securely; never hotlink untrusted URLs.
- **Email change requires re-verification.** Send a confirmation link to the **new** address and keep
  the old one active until confirmed. Never switch silently — that's an account-takeover vector.
- **Password change** requires the **current** password, a confirmed new password, and a strength
  indicator. Optionally invalidate other sessions after a change.
- **Never display secrets** — no passwords, tokens, or full card numbers. Mask sensitive PII where it
  isn't needed in full.
- **Active sessions/devices** — list them (device, rough location, last active) and allow "sign out
  other sessions".
- **Account deletion vs deactivation** — offer both. **Delete** is irreversible: require explicit
  confirmation (re-enter email or type a word), and state exactly what is deleted vs retained for
  legal reasons. **Deactivate** is reversible.
- **Data export** — self-service download of the user's data (GDPR portability). Put it in Privacy &
  data.
- **Feedback** — optimistic save with a success toast; inline field validation; loading/disabled
  states on async actions; never lose input on error.
- **Accessibility** — real `<label>`s, logical focus order, ≥44 px targets, 4.5:1 contrast, no
  color-only signaling.
- **Responsive** — single column on mobile; a sticky save bar for long forms.

### Anti-patterns
- One giant ungrouped page of fields.
- "Delete account" as a tiny link with no confirmation.
- Email change without re-verification.
- Showing the current password.
- A "Save" that silently fails or reloads without feedback.

---

## 2. Logout

### Placement (required)

- The **Logout button lives inside the user-profile menu** — the account dropdown in the header
  (top-right by convention) — and is the **last item** in that dropdown, after Profile, Settings, and
  Help. This follows **Serial Position** (terminal action at the periphery) and **Jakob's Law**
  (standard placement).
- Optionally also expose it under Settings → Account, but the dropdown's last item is the primary
  location.

### Confirmation dialog (required)

Clicking Logout opens a **confirmation dialog** — never an instant logout:

- **Title:** "Log out?"
- **Body:** a short reassurance, e.g. "You'll need to sign in again to access your account."
- **Reason dropdown (select):** "Why are you logging out?" with options such as:
  - Just finished
  - Switching accounts
  - Privacy / security concerns
  - Too many notifications
  - Found a bug
  - Prefer not to say *(default)*
  - Other
- **Buttons:** `Cancel` (secondary, **safe default, autofocused**) and `Log out`
  (primary/destructive).
- **Accessibility:** `role="dialog"` + `aria-modal`, focus trap, `Esc` cancels, focus returns to the
  trigger on close.

### Persist the reason, then invalidate server-side (required)

On confirm, send the reason **with** the logout request:

```
POST /auth/logout
{ "reason": "switching_account" }
```

The backend must:

1. **Record the reason** against the user/session, e.g.:

   ```
   logout_events
     id            uuid
     user_id       FK
     reason        enum(finished | switching_account | privacy_security | notifications | bug | prefer_not_to_say | other)
     session_id    which session ended
     created_at    timestamp
   ```

2. **Invalidate the session server-side** — revoke the token/session, clear cookies, and optionally
   all sessions. Client-side clearing alone is **not** logout.
3. Respond, then the client redirects to a public page (login or home) and shows a brief confirmation.

**Rules:**
- The reason is **optional** — never block logging out on it. Store `prefer_not_to_say` if skipped.
- Treat the reason as **optional analytics/feedback** and disclose it in the privacy policy.
- Use **POST** (not a GET link) so logout can't be triggered by prefetch/CSRF accidentally, and
  protect the endpoint with CSRF protection.
- Send `Cache-Control: no-store` on authenticated pages so the browser Back button can't restore the
  dashboard after logout.

### Anti-patterns
- Logging out instantly on click with no confirmation.
- Clearing only client state while the server session stays valid.
- A plain `<a href="/logout">` GET link.
- Hiding logout somewhere only power users find.
- Making the reason mandatory or blocking logout until a reason is chosen.

---

## 3. Legal & support pages (required when authentication exists)

If the product has **accounts, login, or collects personal data**, it must ship and link these:

### Required pages

- **Privacy Policy** — what personal data you collect, why (the lawful basis), retention periods, who
  you share it with (processors), how users exercise their rights, contact details, cookie use, and an
  effective date + version.
- **Terms of Agreement (Terms of Service)** — eligibility, account responsibilities, acceptable use,
  IP ownership, payment terms (if any), liability limits, termination, dispute resolution, governing
  law, effective date + version.
- **GDPR sections** (for EU/UK users) — lawful basis per processing activity; data-subject rights
  (access, rectification, erasure, restriction, portability, object); DPO/representative contact;
  international transfers and safeguards; **granular cookie consent**; the data-breach process.
- **Support page** — a contact method (form or email), a short FAQ, expected response time, and links
  to the help center/status page.

### Placement & access rules

- Link the legal pages in the **site footer on every page**, *and* at the point of signup
  ("By creating an account you agree to the **Terms** and **Privacy Policy**", with links).
- They must be reachable **before** account creation — never behind a signup wall.
- Legal pages must be **readable and accessible**: real headings, adequate contrast, no tiny grey
  text, no dark patterns.
- Show **effective date + version**; notify users of material changes (email / in-app banner).
- **Cookie consent** (where required): a banner with **granular** choices and **equal-prominence
  accept/reject**, no pre-ticked boxes; remember the choice; link to the policy.
- Provide **self-service data rights** in the profile — export and delete.

### Anti-patterns
- Policies that are unreachable, hidden, or only visible after login.
- Pre-ticked consent, or an "Accept all" only path.
- No contact/support route.
- Terms that contradict the privacy policy.

---

## Checklist

- [ ] Profile grouped into ≤5 sections; email change re-verifies; password change requires current.
- [ ] Delete account is confirmed, explains consequences, and is separate from deactivate.
- [ ] Data export and active-session revocation are available.
- [ ] Logout is the **last item in the profile dropdown** and opens a **confirmation dialog**.
- [ ] The dialog has a **"why are you logging out?"** select whose value is **saved in the DB**.
- [ ] Logout **invalidates the session server-side** and returns a public page.
- [ ] Reason is optional; `prefer_not_to_say` stored when skipped; disclosed in the privacy policy.
- [ ] Privacy Policy, Terms, GDPR sections, and a Support page exist, are linked in the footer **and**
      at signup, and are reachable before account creation.
- [ ] Cookie consent is granular with equal-prominence accept/reject.
- [ ] Legal pages show an effective date + version.
