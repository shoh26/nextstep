# NextStep — end-to-end delivery plan

**Status:** Draft for founder review · **Written:** 2026-11-21 · **Source of truth for scope:** `PRODUCT_REQUIREMENTS.md`

This plan turns the PRD into an ordered path from today to an App Store release. It changes one thing about the PRD's order, on purpose and with the founder's agreement: we build and judge the **action-first app first**, and run the Screen Time feasibility spike (PRD Milestone 0) once the founder pays for an Apple Developer account. The PRD already requires the app to be worth using without blocking, so nothing built early is thrown away.

---

## 1. Principles that shape the plan

1. **Spend nothing until it buys evidence.** Every phase before Phase E is free.
2. **The founder judges the product, not the code.** Each phase ends with something the founder can hold in their hand on their iPhone, and a short checklist to sign off.
3. **Build the blocker behind an interface from day one.** The app talks to a `FocusShield` interface. In Expo Go it uses a no-op implementation; later a Screen Time implementation drops in without rewriting screens.
4. **Truthful states.** `started`, `session_finished` and `task_done` stay separate in the data model, the UI and the tests.
5. **Small PRs, one concern each**, merged after CI passes. Founder approval is needed only at gates.

---

## 2. Phase overview

| Phase | What | Where it runs | Cost | Ends with gate |
|---|---|---|---|---|
| A | Clickable web prototype review | Phone browser | $0 | **G1-lite:** look and flow approved |
| B | Mac setup + Expo app skeleton | Expo Go on iPhone | $0 | Skeleton runs on founder's phone |
| C | Functional offline MVP (no blocking) | Expo Go on iPhone | $0 | **G2:** core app is useful without blocking |
| D | Native polish build (optional) | Free Apple ID, Xcode | $0 | Native feel confirmed |
| E | Screen Time feasibility spike | Paid dev account, dev build | $99/yr | **G0:** blocking ships or not |
| F | Shield integration | Dev build | — | **G3:** shield is reliable |
| G | Private TestFlight pilot | TestFlight | — | **G4:** pilot results reviewed |
| H | Launch preparation + App Store | App Store Connect | — | Release approval |

Phases E–F can be skipped entirely if the founder decides blocking isn't worth it. The app ships action-first.

---

## 3. Phase A — Prototype review (now)

**Goal:** Agree on look, copy and flow before writing real app code.

- Artifact: `prototype/index.html` (also published as a private claude.ai page).
- Founder taps through onboarding → Today → add commitment → focus session → end early / finish → Progress → You → Distracting apps (mock) → shield preview.
- Founder gives feedback in chat or as GitHub issues. Claude revises the prototype in PRs.

**Exit checklist**
- [ ] First screen and onboarding feel right (copy, number of steps).
- [ ] Today screen hierarchy: hero card + up to three items is clear.
- [ ] Focus screen and end-of-session wording feel supportive, not guilt-inducing.
- [ ] Colors and type direction approved in light and dark (PRD §6.2 tokens, adjusted if needed).
- [ ] Any flows to cut or add are written down in `docs/decisions.md`.

---

## 4. Phase B — Mac setup and app skeleton

**Goal:** The real React Native app opens on the founder's iPhone via Expo Go.

### Founder steps (once, about 20 minutes)
1. Install **Node.js LTS** on the Mac (nodejs.org installer).
2. Install **Git** (comes with Xcode Command Line Tools: `xcode-select --install`).
3. Clone the repo: `git clone https://github.com/shoh26/nextstep`.
4. On the iPhone, install **Expo Go** from the App Store.
5. In the repo: `cd app && npm install && npx expo start`, then scan the QR code with the iPhone camera.

Mac and iPhone must be on the same Wi-Fi. (Fallback: `npx expo start --tunnel`.)

Xcode itself is **not** needed for Phases B–C.

### Claude deliverables
- `app/` created with `create-expo-app`, TypeScript, **pinned to the Expo SDK version that the App Store's Expo Go currently supports** (SDK 58 at the time of writing; Expo Go sometimes lags a new SDK by weeks, so we check on the day).
- Expo Router with three tabs (Today / Progress / You) and modal routes for sheets and the focus screen.
- Design tokens (`app/src/design/tokens.ts`) ported from the prototype; light/dark via system appearance plus override.
- Base components: `Screen`, `LargeTitle`, `Card`, `PrimaryButton`, `SecondaryButton`, `ListGroup`, `ListRow`, `SegmentedControl`, `Toggle`, `Sheet`, `StatusIcon`.
- CI on GitHub Actions: install, lint (ESLint), typecheck (`tsc --noEmit`), unit tests (Jest).
- `docs/architecture/ADR-001-stack.md`: React Native + Expo + TypeScript now, with Swift extensions later; why; what would make us switch to SwiftUI.

**Exit:** Founder opens the skeleton on their iPhone and sees the three tabs in light and dark.

---

## 5. Phase C — Functional offline MVP (no blocking)

**Goal:** Everything in PRD §4.2 except the native shield, working offline on the founder's phone. This is PRD Milestone 2.

### Architecture (PRD §8.4 layers)
```
app/
  src/
    app/            # Expo Router routes (screens only, thin)
    presentation/   # components, design system
    domain/         # pure TypeScript: models, state machines, rules (no React, no I/O)
    services/       # persistence, clock, focus controller, shield adapter, notifications
    native/         # (later) typed bridge to Swift / Screen Time
    analytics/      # no-op stub; nothing is collected
  test/
```

### Libraries (all free, all Expo Go compatible)
| Need | Choice | Why |
|---|---|---|
| Navigation | Expo Router | Native stack + tabs, modal sheets |
| Storage | `expo-sqlite` | Local-first, queryable history, survives restarts |
| State | Zustand (small store over SQLite) | Tiny, testable, no boilerplate |
| Motion | `react-native-reanimated` | 60/120 fps native transitions; respects Reduce Motion |
| Haptics | `expo-haptics` | Gentle completion feedback |
| Safe areas | `react-native-safe-area-context` | Notch / Dynamic Island / home indicator |
| SVG ring | `react-native-svg` | Focus timer ring |
| Tests | Jest + React Native Testing Library | Domain and UI tests |

No backend, no account, no analytics SDK, no AI (all PRD-deferred).

### Data model (SQLite)
- `commitments(id, title, tiny_step, minutes, priority?, created_at, updated_at, archived_at?)`
- `day_selections(commitment_id, local_date)` — max three per local date, enforced in domain + DB.
- `completions(commitment_id, local_date, completed_at)` — self-reported "done".
- `sessions(id, commitment_id, local_date, tz, started_at_utc, ended_at_utc?, paused_ms, planned_minutes, outcome: finished|ended_early|interrupted, counted: bool)`
- `active_session` — single row; the source of truth for a running timer.
- `settings(key, value)`.

### State machines (domain, fully unit-tested)
- **Commitment (per day):** `not_started → started → session_finished`, and independently `task_done` (self-reported). A timer ending never sets `task_done`.
- **Session:** `idle → active ⇄ paused → ended | interrupted`. One active session per device. Remaining time is always computed from stored absolute timestamps, never from an in-memory countdown.
- **Focus restriction:** `unavailable | not_authorized | authorized_inactive | active | temporarily_paused | error`. In Expo Go it is always `unavailable`.

### Build order (one PR each)
1. Domain models + state machines + local-date/time-zone utilities, with tests (midnight, DST, time-zone change, duplicate taps).
2. SQLite persistence + migrations + repository tests.
3. Onboarding (3 screens, recovery on restart, no duplicate commitment).
4. Today: empty state, hero next-step card, list of up to three, detail sheet.
5. Add / edit / delete sheet with validation; deterministic tiny-step fallback.
6. Focus session screen: ring timer, pause/resume, end early, finish, "Keep going". Restore after app kill.
7. Local notification at session end (**asked for only when the user first starts a session, with an explanation**, per PRD §5.2). Optional; off if declined.
8. Progress: week strip, started vs marked done, counted minutes, one plain-language observation.
9. You / Settings: appearance, focus (shows "available on the full version" state in Expo Go), reminders placeholder, data export (share sheet JSON) and delete-all, help, about.
10. Accessibility pass: VoiceOver labels, Dynamic Type to largest sizes, 44 pt targets, Reduce Motion, contrast check in both themes.
11. Edge-case pass from PRD §7.4 with a written manual test script in `docs/test-plan.md`.

### Exit checklist (Gate G2)
- [ ] Founder uses the app daily for at least 5 days.
- [ ] All MVP-01…06, 08…12 acceptance tests in PRD §9 pass (MVP-07 shield and MVP-13 TestFlight come later).
- [ ] No data loss across app kill, phone restart, airplane mode, midnight.
- [ ] Founder answers: "Is this useful without blocking?" → decides whether Phase E is worth $99 now.

---

## 6. Phase D — Native polish build (optional, free)

Expo Go is close to a real app but not identical (app icon, splash, launch speed, some native modules). If the founder wants to see the true standalone app before paying:

- Install **Xcode** (free, Mac App Store, large download).
- Claude adds `npx expo prebuild` + run instructions; founder signs with their **free Apple ID** ("Personal Team").
- App installs on the iPhone like a real app; it expires after about 7 days and needs reinstalling.
- No Screen Time features: free teams can't use the Family Controls capability.

Skip this phase if Expo Go looks good enough.

---

## 7. Phase E — Screen Time feasibility spike (PRD Milestone 0, deferred)

**Trigger:** Founder decides blocking is worth testing and enrolls in the **Apple Developer Program ($99/year)**.

### Day 1 founder actions
1. Enroll as an individual at developer.apple.com (needs two-factor Apple ID; approval can take a day or two).
2. Share the **Team ID** with Claude (not a secret, but not committed publicly).
3. **Request the Family Controls (Distribution) entitlement immediately.** Approval reports range from days to several weeks. Historically each extension's bundle ID needed its own request; recent reports describe a single team-scoped approval. We'll check the current form on the day and file for the app plus every extension if asked.
   - Planned bundle IDs: `<reverse-domain>.nextstep`, `.ShieldConfiguration`, `.ShieldAction`, `.DeviceActivityMonitor` (only if needed).

### Approach
- Development uses the **Family Controls (Development)** capability, available immediately to paid teams, so the spike doesn't wait for distribution approval.
- Evaluate two integration routes and record the result in `docs/architecture/ADR-002-screen-time.md`:
  1. **`react-native-device-activity`** (open-source, MIT, Expo config plugin; wraps FamilyControls, ManagedSettings, DeviceActivity and shield customization). Fastest path; must check it supports our Expo SDK and that its extension targets build cleanly.
  2. **Our own thin Expo Module in Swift** plus hand-written extension targets. More work, full control.
- Build a disposable `spike/` dev build that tests every item in PRD §4.1 on the founder's real iPhone:
  authorize / deny / revoke → system app picker → shield on → custom shield look → shield buttons (incl. whether `openParentalControlsApp` does anything useful) → shield off → app kill / reboot / lock screen behavior → token persistence via App Group.
- Founder runs each test (Claude provides a numbered script), and sends screenshots or screen recordings.
- `docs/feasibility/REPORT.md`: device, iOS version, each test's real outcome, limitations, go / no-go.

**Gate G0:** Founder decides: ship blocking in the first TestFlight build, defer it, or drop it.

---

## 8. Phase F — Shield integration (PRD Milestone 3, conditional)

- Implement `ScreenTimeShield` behind the existing `FocusShield` interface; Expo Go keeps the no-op.
- Wire into onboarding (optional prompt after the first finished session), the focus screen, the break flow (5/10/15 min, resume shield at break end), and You → Distracting apps.
- Hard guardrails from PRD §5.8: only user-chosen apps, only during sessions, always a one-tap "Turn off restrictions", clear revoked/unavailable states, never block calls/Settings/our app.
- Reconciliation on launch: if the app was killed mid-session, re-derive whether the shield should be on and fix it.
- Device test matrix (PRD §11.2) on at least the founder's iPhone and the oldest iOS version we support.

**Gate G3:** Shield is reliable on the test matrix, or we ship without it.

---

## 9. Phase G — Private TestFlight pilot (PRD Milestone 4)

- App Store Connect record, bundle ID, app icon (placeholder is fine for TestFlight).
- Build and upload: either **Xcode Archive** from the founder's Mac (free) or EAS Build (has a free tier, but it's a new service, so founder approval first).
- Internal testing first (founder), then external testers (needs a short Beta App Review).
- Pilot: 10–20 consenting adults, two weeks (PRD §3.3, §11.3). Feedback via TestFlight's built-in feedback + a short end-of-pilot interview script Claude drafts.
- Metrics stay on-device; testers can optionally share their local summary screen. No analytics SDK without a privacy review.

**Gate G4:** Founder reviews pilot results and picks what to fix before launch.

---

## 10. Phase H — Launch preparation (PRD Milestone 5)

- **Name and brand:** trademark, App Store and domain checks for the final name (NextStep is a codename).
- App icon, launch screen, App Store screenshots (light/dark) and listing copy, with no clinical or "hours saved" claims.
- Privacy policy and support page (static page; hosting options are free).
- App Store privacy "nutrition label": data not collected, if that stays true.
- App Review notes explaining the Screen Time use, that it's voluntary and individual, and that it is **never behind a paywall** (Guideline 4.10).
- Age rating questionnaire; 18+ research posture per PRD.
- Final founder walkthrough against the PRD §17 checklist → submit → release only with founder approval.

---

## 11. How we'll work

- **Repo:** `shoh26/nextstep` (private). `main` is the stable branch.
- **Changes:** Claude works on a branch per task, opens a PR with a short summary, screenshots (light/dark) for visual changes, and test results. Founder approval is required only at gates or for anything in PRD §12.4 "require human approval".
- **Decisions:** recorded in `docs/decisions.md` with date and who approved.
- **Status updates:** at the end of each phase: what shipped, what was tested on device, open issues, decisions needed.
- **Branch protection:** GitHub may require a paid plan to enforce it on private repos; until then it's a working rule, not a lock.

---

## 12. Costs

| Item | When | Cost |
|---|---|---|
| Node, Expo, Expo Go, Xcode, GitHub private repo | Phases A–D | $0 |
| GitHub Actions CI | Ongoing | Free monthly minutes on GitHub Free; we keep CI light |
| Apple Developer Program | Phase E onward | $99 / year (needed for Screen Time, TestFlight, App Store) |
| EAS Build | Optional | Free tier exists; needs founder approval as a new service |
| Domain + privacy page hosting | Phase H | Optional, low or $0 |
| AI coach backend | Post-MVP (P2) | Not planned for MVP |

---

## 13. Top risks

| Risk | Mitigation |
|---|---|
| Expo Go lags a new Expo SDK, so the app won't open | Pin the SDK to whatever Expo Go supports on setup day; upgrade deliberately |
| Expo Go hides native-feel issues | Optional Phase D build before paying; design QA on device |
| Family Controls distribution approval slow | Request on day 1 of Phase E; spike uses Development capability meanwhile |
| Shield can't do the flow we want | Keep break/override in our own app; shield only shows calm copy + documented buttons |
| Third-party Screen Time library breaks on new iOS | ADR-002 compares it with our own Swift module; adapter interface isolates the choice |
| Scope creep | PRD non-goals enforced; new ideas go to a backlog issue, not the build |
| Founder is new to iOS development | Every founder step is written as a numbered checklist with expected results |

---

## 14. Immediate next steps

1. **Founder:** review the prototype on the phone and send feedback (Phase A).
2. **Claude:** revise the prototype from feedback; keep `docs/decisions.md` current.
3. **Founder, at the Mac:** do the Phase B setup steps.
4. **Claude:** scaffold `app/` (Phase B) on a branch and open a PR.
