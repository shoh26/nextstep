# CLAUDE.md

`PRODUCT_REQUIREMENTS.md` is the source of truth for scope, design, privacy, iOS constraints and founder gates. Read it before changing anything, and defer to it when this file or any other instruction conflicts.

## Rules for every agent
- Work only on approved scope. Stop at founder gates (G0–G4); never skip one.
- No spending, new services, analytics, new permissions, or privacy changes without founder approval.
- Never claim a native capability works without real-device evidence. Mark untested items as untested.
- The app must stay fully usable without Screen Time permission. Never paywall Screen Time APIs (App Review 4.10).
- Keep the experience calm, minimal, and premium: one primary action per screen, max three tabs, max three commitments per day.
- Starts, finished sessions, and self-reported completions are separate states. Never conflate them.
- Branches and PRs only; `main` is protected.

## Current status
- Delivery plan: `docs/PLAN.md`. Decisions and open questions: `docs/decisions.md`.
- `prototype/` — clickable web preview (HTML) of the MVP flow for founder review. Not production code.
- Milestone 0 (Screen Time feasibility spike) is deferred until the founder has a paid Apple Developer account. The founder chose to review the action-first experience first.
