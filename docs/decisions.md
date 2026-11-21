# Decision register

Product and technical decisions, with dates and who approved them. Open items are not approved until moved to "Decided".

## Decided

| ID | Date | Decision | Approved by |
|---|---|---|---|
| D-001 | 2026-11-21 | Private repo `shoh26/nextstep`; PRD is the source of truth. | Founder |
| D-002 | 2026-11-21 | Build and review the action-first app first; run the Screen Time spike (PRD Milestone 0) after the founder enrolls in the paid Apple Developer Program. | Founder |
| D-003 | 2026-11-21 | Phase A uses a clickable HTML prototype (`prototype/`) styled to mimic a native iPhone app, viewable from a phone. | Founder |
| D-004 | 2026-11-21 | Phases B–C run in Expo Go on the founder's iPhone (free, no Xcode needed). | Founder (proposed in `docs/PLAN.md`; confirm at review) |

## Proposed defaults (awaiting founder review)

| ID | Proposal | Why |
|---|---|---|
| P-001 | React Native + Expo + TypeScript; Swift only for Screen Time extensions (ADR-001 to confirm). | Founder knows React/TS; PRD default. |
| P-002 | Pin Expo SDK to the version Expo Go on the App Store supports on setup day. | Otherwise the app won't open in Expo Go. |
| P-003 | Local storage with `expo-sqlite`; no backend, no account, no analytics in MVP. | PRD §8.5, §3.4. |
| P-004 | `FocusShield` interface with a no-op implementation until Phase F. | Lets blocking drop in without rewriting screens. |
| P-005 | Minimum iOS version decided in Phase E from verified API availability (PRD §14.3). | Avoid hardcoding an unverified target. |
| P-006 | Notifications asked for only at the first session start, with an explanation; off if declined. | PRD §5.2, §5.11. |
| P-007 | CI with GitHub Actions: lint, typecheck, unit tests. | Free; PRD Definition of Done. |

## Open questions

| ID | Question | Needed by |
|---|---|---|
| Q-001 | Prototype feedback: anything to cut, add or restyle? | End of Phase A |
| Q-002 | Is the app useful without blocking? Pay $99 for the Screen Time spike? | Gate G2 |
| Q-003 | Reverse-domain bundle ID prefix (e.g. `com.<yourname>.nextstep`). | Phase D or E |
| Q-004 | Final product name. | Phase H |
