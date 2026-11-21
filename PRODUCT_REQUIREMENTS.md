# PRODUCT REQUIREMENTS DOCUMENT (PRD)
## Project: NextStep — Working codename, NOT a final brand name
**Product category:** Consumer iPhone app / intentional action and digital well-being  
**Document version:** 1.0  
**Prepared:** November 21, 2026  
**Status:** Product direction approved in principle; implementation details and high-risk platform features require validation  
**Audience:** Founder / stakeholder; ChatGPT acting as product and UX lead; Claude Code acting as technical lead and implementer  
**Primary platform:** iPhone, iOS first  
**Source of truth:** This file in the private GitHub repository; changes proposed by pull request and recorded in a changelog or decision log.

> **IMPORTANT FOR CLAUDE CODE:** Treat this document as product requirements, not blanket authorization to implement every idea or purchase services. Work in phases; **begin with the technical feasibility spike and architecture proposal**. Build the approved MVP before post-MVP concepts. Raise blockers and design tradeoffs, do not quietly claim unsupported capabilities, and obtain explicit founder approval at designated gates. Prefer a finished, tested, beautiful minimal experience over lots of features.

---

# 0. Executive summary

We want to help someone who **knows what matters to them but keeps postponing it**, often because effortless distractions (Instagram, TikTok, YouTube, games, or general phone use) deliver easier short-term rewards.

**One-sentence pitch:** An elegant iPhone action coach that helps users turn intention into action with a tiny next step, optional distraction friction, and encouraging, truthful progress.

**North star:** Increase the number of meaningful, self-chosen actions users actually start and follow through on. Reduced *unintentional* scrolling is an important secondary outcome, not the only goal.

**Core loop:**
1. Choose up to three meaningful commitments for today.
2. See ONE clear next action; make the first step small enough to start.
3. Start a short focus/action session with one tap.
4. Optionally shield personally selected distracting apps while focusing.
5. Finish or end the session honestly, record progress, and move on with life.
6. Reflect gently; adjust tomorrow without shame.

**Critical differentiator to test:** Unlike a conventional to-do list or pure screen-time blocker, our emphasis is the **transition from avoiding a task to starting it**. Competitor solutions already offer blocking, breath pauses, and habit-to-unlock; do NOT claim invention or unique IP without research.

**Design mandate:** Premium, serene, extremely simple, effortless for nontechnical users, excellent accessibility, one primary action per screen, few decisions, no clutter, no shame, no addictive engagement mechanics. The app must *help people leave the app and live their lives.*

**Commercial hypothesis:** Potential freemium product later, but no pricing or paywall in the initial MVP. Apple App Review Guideline 4.10 prohibits monetizing access to built-in Screen Time APIs; do not gate the native Screen Time capability behind a charge. Any later paid tier must sell distinct value such as genuinely advanced coaching/service and undergo legal/App Review review.

---

# 1. Vision, mission, principles

## 1.1 Vision
A world where a person's phone supports the life they want rather than taking over the time they meant to spend on it.

## 1.2 Mission
Make intentional action easier, especially at the moment someone feels resistance, overwhelm, uncertainty, or an urge to scroll instead.

## 1.3 User promise
- "I can decide what matters today in less than a minute."
- "I immediately know my next small step."
- "I can get started without feeling I need to finish everything."
- "When I'm tempted to scroll, I get a fair chance to choose intentionally."
- "I'm treated like an adult; I can rest or override without guilt."
- "My progress is real and my private habits stay private."

## 1.4 Non-negotiable principles
1. **Clarity before features:** Every visible element earns its place.
2. **One next step:** Prioritize a single action above a crowded to-do list.
3. **Autonomy over punishment:** User can stop/pause/disable restrictions; no manipulative lock-in.
4. **Compassionate tone:** Never call users lazy or label them failures; avoid streak loss/guilt loops.
5. **Do less, better:** Start with small, reliable feature set; intentionally defer speculative extras.
6. **Native quality:** Fluid, elegant, feels correct on an iPhone, not a web page squeezed onto a phone.
7. **Truthful feedback:** Never claim task completion was verified if self-reported, or time was "saved" if not measured.
8. **Privacy by default:** Keep data on device unless there is a clear user benefit to synchronization.
9. **Progressive permission:** Explain a feature before requesting system authorization.
10. **Accessible and inclusive:** Dynamic Type, VoiceOver, contrast, Reduce Motion, no reliance on color alone.

---

# 2. Problem and audience

## 2.1 Main problems
- **Intention-action gap:** Users intend to do meaningful tasks but fail to begin.
- **Avoidance:** Tasks feel large, vague, uncomfortable, boring, or uncertain.
- **Unintentional scrolling:** Users enter a social or entertainment app automatically and lose track of time.
- **Too much productivity overhead:** Existing systems ask users to organize so much that the system itself becomes work.
- **Shame cycle:** Strict streaks and warnings can worsen avoidance rather than support it.

## 2.2 Primary audience (for product research)
- Adults 18+ with an iPhone who frequently procrastinate on personally meaningful activities and/or get pulled into mindless mobile scrolling.
- People who want a gentle behavioral support tool, not a complex project manager.
- People who prefer premium, calming design and low setup effort.

**V1 language/market:** English (US), consumer iPhone, no child/parent monitoring or multi-user family control UI in MVP.

## 2.3 Example jobs-to-be-done
- "When I reach for Instagram instead of beginning work, help me pause and start just two minutes."
- "When my to-do item is vague, help me identify one concrete action."
- "When I have 20 spare minutes, remind me of the goal I myself chose, without nagging."
- "When I need a break, let me choose one consciously and return without shame."
- "When I finish a small step, help me recognize it as legitimate progress."

## 2.4 Anti-personas / not initially targeted
- Employers monitoring employees.
- Parents administering restrictions for children.
- Clinicians providing treatment for ADHD or mental-health conditions.
- Heavy enterprise task-management use cases.
- Users seeking unbreakable/irreversible device restrictions.

## 2.5 Product positioning
**Category:** Action-first digital well-being.  
**Not:** Another generic todo list, full calendar, therapy app, extreme blocking app, or motivational quote feed.

---

# 3. Success criteria and measurement

## 3.1 North-star metric
**Meaningful Starts per Active User per Week (MS/AUW):** Number of distinct user-chosen commitments for which a user explicitly starts a micro-action or focus session in a week. Count actual starts, not mere app opens. Present metric as product telemetry, not objectively verified behavior.

## 3.2 Supporting metrics
- **Activation:** Percentage of new users who create >=1 commitment and initiate >=1 action session during their first day.
- **Follow-through:** Percentage of selected commitments marked completed (self-reported) within a day/week.
- **Return behavior:** D1, D7, D14 retention (if opted-in analytics can support measurement).
- **Focus completion:** Sessions started, deliberately finished, interrupted, abandoned; distribution of session lengths.
- **Distraction intervention:** Number of shield encounters and outcomes **only if supported/available without violating Screen Time privacy restrictions**; never invent per-app events.
- **Perceived effect:** Opt-in "Did this help you start?" lightweight question, no more than occasional prompt.
- **Sentiment:** Ease of use, sense of control, felt pressure, and likelihood of recommendation from interviews.
- **Reliability:** Crash-free sessions, authorization/extension failure rates (aggregate, privacy-safe).

## 3.3 Pilot acceptance targets (hypotheses, not promises)
Test with approximately 10-20 consenting adult users for two weeks. Determine whether:
- Most testers can create a commitment and start their first action without explanation.
- The essential flow is typically understandable within 30 seconds of exploration and onboarding can be completed quickly.
- A substantial share (initial target: >=60%) of pilot testers voluntarily start meaningful actions on at least three days during week 2.
- Most interviewed users describe the product as calmer/simpler than their existing methods.
- iOS restriction capability performs consistently for the selected device/OS test matrix.

Do not present these targets as statistically validated or clinical efficacy. If we miss them, inspect data and feedback before adding features.

## 3.4 Event taxonomy (privacy-conscious)
All events should be aggregate/non-sensitive by default and collected only if analytics is enabled:
`onboarding_started`, `onboarding_completed`, `commitment_created`, `commitment_selected_today`, `action_started`, `action_paused`, `action_finished`, `action_abandoned`, `commitment_self_reported_done`, `focus_enabled`, `focus_disabled`, `authorization_requested`, `authorization_granted`, `authorization_denied`, `shield_rule_activation_failed`, `feedback_submitted`.

Never include free-text task titles, prompt contents, selected app names, Screen Time tokens, personally sensitive notes, or detailed usage histories in analytics. No analytics SDK until a privacy review. Local counters are sufficient for alpha.

---

# 4. Product scope and prioritization

## 4.1 P0 — FIRST: technical feasibility spike, before polished implementation
Goal: prove or disprove our core iOS blocker/intervention experience on a **real iPhone**, under Apple-supported APIs and approval constraints.

Deliverable:
- Minimal Xcode/Expo proof of concept (not a production app) demonstrating:
  1. Request voluntary individual Family Controls authorization.
  2. Let the user select apps with Apple's system FamilyActivityPicker.
  3. Apply/remove a ManagedSettings shield to those selections during a focus interval.
  4. Show a customization through ManagedSettingsUI/Shield Configuration Extension (subject to API limitations).
  5. Check Shield Action handling, including whether an officially supported `openParentalControlsApp` flow works on target OS/deployment; provide safe fallback if it doesn't.
  6. Persist selected opaque tokens locally or in approved app-group storage as appropriate and correctly handle revoked authorization.
  7. Test scheduling, transitions, locked phone/background state, app restart, and uninstall/removal behavior.
  8. Document app and extension entitlement requirements, provisioning, distribution request process, and App Review risk.
- A short written feasibility report with screenshots/videos, actual device + OS, API names, reproducible build steps, known limitations, and go/no-go recommendation.

**Gate G0:** Founder approves the architecture and whether blocking is included in first TestFlight build, based on real evidence. If Apple approval/API behavior blocks the intended experience, ship a valuable **action-first MVP without app blocking** rather than stalling or using private APIs.

## 4.2 P1 — MVP (ship a coherent iPhone beta)
1. Small, visually excellent onboarding; no account required.
2. Create/edit/delete commitments; choose up to three for Today.
3. One prominently recommended next action; deterministic tiny-step suggestions.
4. Quick focus/action session (default 5 min, options 2/5/10/20 min) with start/end.
5. Optional native distraction shield during a focus session, **only after P0 validation and entitlement readiness**.
6. Gentle break/override pathway; user always able to disable restrictions.
7. Lightweight, truthful daily/weekly progress.
8. Settings: appearance, notifications opt-in, restrictions, privacy/data export/delete, help.
9. Basic accessibility, failure states, offline persistence and reliability.
10. TestFlight-ready build; functional and design QA.

## 4.3 P2 — After the MVP shows value
- AI action coach (suggest micro-steps and reframe overwhelming tasks).
- Context-sensitive personalized interventions and optional recurring routines.
- Optional notification nudges, scheduled commitments, and widgets.
- Better trend summaries based on trustworthy available data.
- Account-based backup/sync only if needed and consented to.
- Carefully designed paid service tier **excluding paywalling Apple Screen Time API access**.

## 4.4 P3 — Exploratory / NOT authorized for immediate build
- Accountability partners and consent-based sharing.
- Adaptive coaching based on user patterns, privacy safe.
- Apple Watch companion, Android, calendar integration, Siri/Shortcuts.
- Advanced analytics and experiments, contextual recommendations.
- Gamification only if validated as supportive rather than addictive.

## 4.5 Explicitly OUT OF SCOPE for MVP
- Social feed, chat community, public leaderboard, viral loops.
- Huge backlog/project-management workflows, subtasks hierarchy, Kanban, complex tags.
- AI chatbot as the home screen.
- Mandatory account creation or collecting contacts.
- Calendar/email/social account scraping or monitoring personal browsing.
- Clinical diagnoses, ADHD treatment claims, medical advice.
- Detecting the content of social feeds or arbitrary overlays on top of other apps.
- Claiming the app can prevent all bypasses, force task completion, or operate as an always-on unrestricted background agent.
- Subscriptions, ads, referral incentives, manipulative urgency prompts.

---

# 5. Core experience and information architecture

## 5.1 Navigation
At most THREE main destinations:
1. **Today** — main experience: next step, a tiny action, today's up-to-three commitments.
2. **Progress** — minimal, reassuring summary; not a data dump.
3. **You** — preferences/settings, privacy, focus permissions.

Do not add a separate tab for a chatbot, task backlog, or notifications. Use a clean sheet/modal for adding and editing a commitment. If a backlog exists, keep it behind Today and do not surface clutter.

## 5.2 First-run onboarding (goal: 60-90 seconds, no permission wall)
- Screen 1: Single attractive statement of value: e.g. "Make starting easier." CTA "Get started." No lengthy carousel.
- Screen 2: Ask "What's one thing you want to make time for?" Example suggestions: move my body; learn something; get an important task done; spend intentional time offline. User can type custom text.
- Screen 3: Ask for smallest starting step or offer simple local default; user can accept/edit. Select an optional time.
- Screen 4: Land on Today with a clear "Start for 5 minutes" CTA.
- After the user understands focus value: optional explanation "Want help avoiding distracting apps during focus?" -> screen-time authorization and Apple picker. Provide "Not now" and remain fully functional.
- Never demand notification permissions, sign-in, location, contacts, microphone, or tracking consent during onboarding.

**Onboarding recovery:** On app restart, continue or restart gracefully without duplicating commitments. Accessible "Skip" where appropriate. Graceful handling of users who decline Screen Time permission.

## 5.3 Today screen, normal state
Structure in visual order:
1. Small, contextual greeting (not overly chatty), calm background, optional subtle date.
2. One strong headline: "One small step is enough." or dynamic copy.
3. **Hero next-step card** with user commitment title, one tiny actionable step, optional suggested duration, one primary CTA **Start**.
4. Minimal "Today" list with max three commitments, clear status, easy tap to change selection.
5. Small tasteful progress indicator (e.g. "1 of 3 started") with accuracy as priority.
6. Bottom navigation (Today / Progress / You).

Zero or one primary CTA visible per content region. Do not stack competing action buttons or expose 20 data points. No confetti by default. No guilt-inducing red badges.

## 5.4 Today screen, empty state
- Headline: "What matters today?"
- Clear CTA: "Add your first commitment".
- Optional one-tap examples (3-4, not a giant catalog).
- No permission prompts, empty graphs, or fake demo analytics.

## 5.5 Commitment model and priority
User's mental model: **things I need, should, or want to do**. Internal product terminology:
- **Commitment:** A meaningful user-selected intention (e.g. "Exercise").
- **Tiny step:** Immediately doable action (e.g. "Put on shoes").
- **Session:** A time-bounded effort on that step/commitment.
- **Progress:** Started, finished session, or self-reported task completion. These are different states.

Fields in local model: `id`, `title`, `tinyStep`, `suggestedDurationMinutes`, `priority?`, `createdAt`, `updatedAt`, `archivedAt?`, `selectedForLocalDate?`, `status`, `completedAt?`.

Priority selection is **optional and hidden by default**: "Important", "Helpful", "Optional" (wording to user test). Avoid presenting complicated Must/Should/Need/Good categories as four mandatory controls. Maximum of three selected Today commitments; allow edit/remove and later selection from simple saved items if needed. User is never forced to assign deadlines.

## 5.6 Add/edit commitment
- Open a small bottom sheet from Today.
- Single required field: "What do you want to do?"
- Optional inline field "What's the smallest first step?" with examples.
- Optional duration selector (2, 5, 10, 20 min); default 5.
- Save CTA; keyboard, autofocus, safe areas, error handling optimized.
- Empty/whitespace-only titles prohibited; cap sensible length with friendly validation.
- Support edit, delete, mark done, re-open; destructive delete confirmation only when meaningful.
- Avoid noisy priority controls, due dates, and recurrence until evidence justifies them.

## 5.7 Action session
- Start with ONE tap from Today.
- Dedicated focus screen: huge but understated timer, one-line tiny step, optional session end and pause.
- Optionally apply selected-app shields to begin and remove them when session ends. User opt-in required.
- Focus session can run with phone locked; persist start timestamp and state; timer calculated from absolute clock timestamps (not fragile JS-only intervals).
- On expiry: gentle haptic (respect settings), notification only if permission; show "You showed up" and choices "Keep going" / "Finish for now".
- On early stop: "That's okay. Want to count the time you put in?" Do not mark entire task done automatically.
- Honest statuses:
  - `not_started`
  - `started` (session began)
  - `session_finished` (elapsed duration)
  - `task_done` (user explicitly marked complete)
- If a user leaves to take an intended break, do not shame them; pause/resume or stop transparently.

## 5.8 Distraction intervention and shield flow
**Desired experience:** While a user intentionally focuses, opening one of their selected distracting apps encounters an Apple-supported shield that prompts a more intentional choice.

**Reality/constraint:** iOS only allows the system shield interface and supported customization properties/actions; it is NOT an arbitrary React Native view drawn over Instagram. The system picker returns opaque app/category/domain tokens. Do not assume we can monitor every launch, retrieve raw app identities, measure exact doomscrolling time, or deep-link directly to a special coaching view without device-level verification. Apple provides `ShieldActionResponse.openParentalControlsApp` in current docs; verify supported OS version, user authorization, and precise behavior before using it.

**Suggested shield copy for prototype (within system-provided customization):**
- Title: "Take a moment"
- Subtitle: "You chose to focus right now. A small step is enough."
- Primary action: "Back to focus" (only if the actual action works within API limitations)
- Secondary action: "Take a break" / "Close" (validate supported action count and semantics)

**Full break/override experience should live in our own app**, not presume an arbitrary multi-button shield. In app, allow 5/10/15 minute break and "Turn off restrictions". Restoring shields after a break should be resilient to background/OS scheduling constraints; disclose limitations honestly.

**Critical guardrails:**
- Restrict ONLY user-selected apps/categories and only in clearly indicated windows.
- Never block emergency services, phone calls, system settings, our own app, or essential user capabilities.
- Always expose a straightforward user-controlled way to stop focus restrictions.
- Respect revoked authorization and uninstall; don't claim unenforceable locks.
- Show clear "Screen Time not enabled" / "Permission revoked" / "Selection unavailable" states.
- Do not demand access to sensitive usage data beyond what's needed.
- Make Screen Time features optional; usable fallback without them.

## 5.9 Intentional break
- User taps "Take a break" inside app; chooses 5/10/15 minutes or ends focus.
- UI is neutral and supportive, not a penalty.
- Resume restrictions at the agreed time when system scheduling supports it; user can cancel.
- Record an intentional break only if helpful, and show it as a valid choice.

## 5.10 Progress page
Keep to 2-3 important insights. For MVP:
- Weekly number of commitments **started** (truthfully measured in app).
- Weekly number of commitments **marked done** (self-report).
- A compact week view showing days with at least one meaningful start.
- Optional plain-language observation: "You started something on 4 days this week."

Do NOT show fabricated "hours saved". DeviceActivity usage reports can be evaluated post-spike, but be transparent about OS-granted scope and caveats. If only local data, stats must derive from local actions only.

## 5.11 You / Settings
- Appearance: System / Light / Dark.
- Focus & distracting apps: authorization state, select apps, enable/disable, visible active period.
- Notifications: only relevant gentle reminders, opt-in; initial MVP may have off by default.
- Data: privacy policy, local export (if feasible), delete all local data, how analytics works.
- Help: contact/support, FAQ, known Screen Time limitations.
- About: version and build number.
- Later: account/sync/subscription (not visible when not implemented).

## 5.12 Copywriting voice
Calm, concise, supportive, adult, not overly therapeutic.

Preferred:
- "Start with two minutes."
- "You can do just the first step."
- "Want a short break instead?"
- "You showed up today."
- "Your focus settings are off. You can turn them on anytime."

Avoid:
- "Stop being lazy!"
- "You failed your streak!"
- "You wasted 3 hours!"
- "You're addicted."
- "Only winners stay consistent."

---

# 6. Visual design and interaction specification

**This is a binding product standard, not optional polish.** Founder has repeatedly emphasized an aesthetically exceptional app with an intuitive UI that anyone can use, not a complicated productivity dashboard.

## 6.1 Art direction
- **Style:** Apple-quality quiet luxury, warm modern minimalism, carefully restrained editorial typography, generous negative space, subtle depth.
- **Emotional tone:** Calm, competent, encouraging, premium, trustworthy, not clinical, childish, gamified or corporate.
- **Theme:** Warm off-white/light default and a refined charcoal dark theme; obey iOS system appearance.
- **Hero principle:** Content hierarchy and typography matter more than decorative elements.
- **Reference inspirations (quality only, not copying):** Apple Health's clarity, Things 3's polish, high-end mindfulness apps' composure. Never copy screens or branding.

## 6.2 Suggested initial design tokens (PROPOSAL: adjust after visual QA)
- `background.light`: `#F8F7F3` — warm porcelain.
- `surface.light`: `#FFFFFF` — white cards.
- `surfaceAlt.light`: `#F0F1ED` — subtle distinction.
- `ink.light`: `#1D2220` — deep soft black.
- `muted.light`: `#656D69` — secondary copy, verify WCAG.
- `accent.primary`: `#3F695B` — muted botanical green; adjust accessible contrast.
- `accent.soft`: `#E3ECE6` — soft green backgrounds, never sole communication channel.
- `background.dark`: `#121716` — charcoal.
- `surface.dark`: `#1C2320` — elevated charcoal.
- `ink.dark`: `#F6F7F3` — warm white.
- `muted.dark`: `#B3BCB6` — subdued high-contrast gray.
- Destructive/error states are discreet but accessible; do not use danger red as motivation.

**Contrast:** Meet at least WCAG AA for body text and controls, in both modes and with Dynamic Type. Tokens are initial directions, not permission to use inaccessible pairings.

## 6.3 Typography
- Prefer iOS system typography / SF Pro via platform fonts for robust rendering and familiarity.
- Large hero headline approx. 30-36 pt in default scale, dynamic type compatible.
- Section heading approx. 18-22 pt; body approx. 16-17 pt; helper text approx. 13-15 pt and accessible.
- Restrained weights; generous line height; avoid all-caps body copy and clipped multi-line tasks.
- SF Symbols consistent stroke weight when practical.

## 6.4 Layout and components
- 8-point spacing system, with intentional 4-point fine adjustments.
- Horizontal margins ~20-24 pt; vertically generous composition.
- Cards with soft radius ~16-22 pt; avoid card overload and nested cards.
- Main CTA 48-56 pt high; minimum interactive hit area >=44 x 44 pt.
- One strong accent color; minimal gradients, no neon.
- Subtle separators; shadows only if they clarify elevation.
- Maximum three persistent tabs. No hamburger menu for daily core tasks.
- Prefer native sheets, safe-area insets, keyboard avoidance, familiar back gestures.

## 6.5 Motion and haptics
- Meaningful transitions ~150-300ms, never animation for animation's sake.
- Gentle completion haptics; no intrusive repeated vibrations.
- Respect `Reduce Motion`, `Bold Text`, larger text, accessibility contrast, `VoiceOver`.
- No blinking or artificial rewards designed to increase app engagement.

## 6.6 Design deliverables and QA expectations
Before implementing full feature flow, provide:
1. A screen inventory with information hierarchy.
2. Low-fidelity flows for approval.
3. At least one polished Today, Focus, Onboarding, Progress, Settings screen example in light and dark.
4. Reusable component library / tokens.
5. Preview screenshots from actual simulator/device at standard and large text sizes.
6. Usability check: can a first-time tester understand the primary action without a tutorial?

**No unapproved design drift:** New navigation or visual complexity requires a product review. A technically working but visually mediocre UI does **not** satisfy acceptance.

---

# 7. Behavior details, rules, and edge cases

## 7.1 Daily reset and time semantics
- Use device locale/time zone; group commitments by local calendar day.
- At local midnight, reset today's selections/status **for daily view only** while preserving historical records.
- Users traveling/timezone switching should not lose/duplicate recorded historical sessions. Store UTC timestamps and local date/timezone context.
- Never silently delete commitments at midnight.
- When app opens after missed days, don't guilt users or flood reminders.

## 7.2 Timer durability
- Use persisted absolute timestamps, not only timers running in JS memory.
- Support backgrounding, screen locking, app termination/relaunch, interruptions (calls, device power off).
- If OS restrictions prevent reliable notification at exact expiry, document behavior and avoid claiming guaranteed alerts.
- Avoid double-counting overlapping sessions; permit one active session per user/device.

## 7.3 State machine (conceptual)
Commitment: `saved -> selected_today -> started -> (session_finished | session_abandoned) -> task_done`.
Session: `idle -> active -> (paused -> active)* -> ended | interrupted`.
Focus restriction: `unavailable | not_authorized | authorized_inactive | active | temporarily_paused | error`.

Transitions must be explicit, testable, and never assume task complete merely because a timer ended.

## 7.4 Edge-case acceptance
- No commitments: purposeful empty state.
- No distractions selected: focus timer works normally.
- Permission declined/revoked mid-session: safe and visible degrade; do not crash.
- App kills/reopens: session state restored/ended safely and restrictions reconciled.
- Device reboots / time changes / daylight saving: no double sessions, wrong remaining minutes, or stuck focus.
- Selected app uninstalled: token/selection reconciliation where possible.
- Phone in airplane mode: core features still work.
- App extension fails or receives unexpected response: fail predictably; user can still recover controls.
- Large text/VoiceOver: primary button and key text remain usable.
- User overrides early: no shame, no fabricated completion.
- User enters long/emoji/RTL task: safe text layout and data validation (full internationalization later).
- Duplicate taps: no duplicate session or entries.

---

# 8. Technical architecture: recommendation, not a forced choice

## 8.1 Default hypothesis
Use **React Native + TypeScript + Expo with a custom native development build**, plus native **Swift** components and Screen Time extensions for capabilities React Native cannot provide. Favor an Expo prebuild/config-plugin strategy only if the native targets and entitlements are stable and reproducible.

**Reason:** The founder is experienced in React/TypeScript; most UI and logic can be maintained quickly, with native Swift where unavoidable.

**Alternative permitted:** Pure SwiftUI if the native extension lifecycle, stability, app quality, or long-term maintenance demonstrably favors it. Claude Code must produce an Architecture Decision Record (ADR) comparing options, with evidence from P0. **No unapproved full-stack framework migration.**

## 8.2 Expected platform components
- `FamilyControls`: voluntary authorization, native app/category/domain picker, opaque tokens.
- `ManagedSettings`: shield selected apps/categories/domains.
- `ManagedSettingsUI`: system-constrained shield appearance.
- `DeviceActivity`: optional schedules/threshold callbacks as technically appropriate.
- Native iOS app extension targets: Shield Configuration, Shield Action, Device Activity Monitor **only if necessary**.
- Shared App Group storage if required for communication with extensions; minimal shared data and strict access.

**Avoid:** Private APIs, extension tricks/URL schemes unsupported by Apple, scraping usage data, Accessibility hacks, arbitrary overlays, jailbreaking, insecure token handling.

## 8.3 Expo / Swift integration notes
- Expo Go is not sufficient for custom Screen Time native code; use a native development build and Xcode/EAS where appropriate.
- Native modules should have a typed, narrow TypeScript interface; no native internals in presentation components.
- Native extensions need their own signing/configuration/entitlements; reproducible build and CI must handle each target.
- Test on physical iPhone. Simulator-only proof is insufficient for authorization and shielding behavior.
- Record specific SDK/API availability and iOS version gates; docs can change.

## 8.4 Suggested app layers
- `presentation`: screen components, navigation, design system.
- `domain`: commitments, tiny steps, session state machine, progress calculations.
- `services`: persistence, focus controller, optional notifications, future coaching.
- `native`: typed iOS adapter + Swift/extension implementations.
- `analytics`: consent-aware optional events; stub/no-op by default.
- `tests`: unit/integration/e2e/native test plans.

## 8.5 Storage and account strategy
**Alpha/MVP default:** Local-first, offline-capable, no sign-up. Choose a maintained encrypted or standard on-device persistence mechanism suitable for the actual sensitivity and queries (SQLite or equivalent); store secrets in Keychain where appropriate. Explain what device backup means and don't promise cross-device sync.

Add Supabase or another backend **only if there's a validated requirement** (e.g. sync, subscription entitlement, optional cloud coach) and approved privacy model. No backend simply because a template includes one.

## 8.6 Future AI coach, API contract (NOT MVP dependency)
- AI calls originate from a secure backend with server-side credentials and rate limits, NOT a hardcoded secret in app bundle.
- Inputs minimized: e.g. user's task and explicitly shared context, not selected app identities or full usage history by default.
- Structured output: `tinyStep`, `rationale?`, `suggestedMinutes`, `fallback?`; validate on server/client; enforce character and token limits.
- AI is advisory, optional, editable; never claims knowledge of the user not provided to it.
- Deterministic fallback when offline, API fails, or model output is unsafe/unhelpful.
- Strong guardrails against manipulative coaching, diagnosis/treatment claims, self-criticism, or unsafe instructions.
- Don't imply coaching prevents ADHD or cures mental-health issues; not a regulated medical product.

## 8.7 Security and privacy
- No required registration for pilot; no raw selected-app data sent to cloud.
- Screen Time tokens treated as private; use purpose-limited storage.
- No third-party ad tracking, data brokers, or analytics with sensitive data.
- Redact identifiers/prompts/screenshots in logs, CI and crash reporting.
- Privacy policy and in-app deletion before public App Store release.
- All network requests TLS; secrets in CI secrets manager; least-privilege tokens.
- User can disable restrictions at any time, withdraw authorization via iOS, and remove local app data.
- Document data collection honestly in App Store privacy labels.
- No child data processing in MVP. Age posture 18+ for initial user research, subject to launch policy review.

## 8.8 Performance and operational quality
- Fast cold start; no spinner for local actions.
- UI remains functional offline.
- Scroll and transitions feel native at typical iPhone refresh rates.
- No unnecessary network dependency for core flows.
- Swift extensions must stay within memory/time constraints.
- Battery-efficient scheduling; avoid polling user activity or aggressive background work.
- Crash logs opt-in/limited and redacted; never send user task text automatically.

---

# 9. Requirements with acceptance criteria

| ID | Priority | Requirement | Minimum acceptance test |
|---|---|---|---|
| P0-01 | Spike | Native individual authorization | On real iPhone, allow/deny/revoke flows documented and handled without crash. |
| P0-02 | Spike | App selection and shields | Select one app via system picker, shield during test focus, remove shield reliably; record limits. |
| P0-03 | Spike | Shield visual/action behavior | Screenshot system shield and test all supported button responses on target OS. |
| P0-04 | Spike | Extension/signing feasibility | Demonstrate repeatable build and list entitlement requests per target. |
| MVP-01 | Must | Low-friction onboarding | User creates and starts first commitment without an account or Screen Time permission. |
| MVP-02 | Must | Create/edit/delete commitments | CRUD persists after restart; input validation and undo/confirmation work. |
| MVP-03 | Must | 3 commitments/day | Today surfaces max 3 without hidden fourth; archived items aren't lost. |
| MVP-04 | Must | Tiny next action | Every selected commitment has a concrete editable micro-step; deterministic fallback. |
| MVP-05 | Must | One-tap action session | Tap Start opens timed session immediately; state survives background/restart. |
| MVP-06 | Must | Accurate progress | Starts, finished sessions, and self-reported completions are separate; counts match data. |
| MVP-07 | Conditional | Native focus shielding | Only if G0 approved; user-selected targets shielded only for agreed periods. |
| MVP-08 | Must | Unrestricted recovery | User can disable any restriction from app; permission errors have recovery instructions. |
| MVP-09 | Must | Premium UX | Light/dark, clear hierarchy, 3 tabs max, no confusing controls; founder visual signoff. |
| MVP-10 | Must | Accessibility | VoiceOver, Dynamic Type, 44pt touch targets, Reduce Motion and contrast audited. |
| MVP-11 | Must | Privacy defaults | Core works without account/cloud; no sensitive data in analytics/logs. |
| MVP-12 | Must | Offline core | Add/start/end/progress work offline; data not lost on restart. |
| MVP-13 | Must | TestFlight readiness | Reproducible signed build, privacy/docs, test matrix, no critical open defects. |
| P2-01 | Later | AI microstep coach | Explicit opt-in; structured, safe, editable output; fallback without AI. |
| P2-02 | Later | Gentle nudges | User-initiated/permissioned, quiet hours, easy mute; no guilt spam. |
| P3-01 | Explore | Accountability | Explicit mutual consent, no private task or usage data shared by default. |

### Definition of Done (all production PRs)
1. Linked to approved issue/requirement and scoped to it.
2. Implemented with clear UX states (loading/empty/error/success) and accessibility labels.
3. Unit/integration test coverage for changed behavior; native smoke test for extension changes.
4. Typecheck/lint/build pass in CI; no secrets or privacy regressions.
5. Screenshots or recordings for visual changes, light + dark.
6. Short QA notes, edge cases, known limitations.
7. Independent review or configured code-review agent feedback resolved or explicitly waived.
8. No production merge/release without required approval.

---

# 10. Development plan and founder review gates

## Milestone 0 — Discovery and technical proof (BLOCKER)
- Verify latest Apple Screen Time capabilities, App Review rules and distribution entitlements.
- Create disposable native proof on physical device.
- Explore React Native/Expo integration stability.
- Deliver risk register, architecture ADR, and feasible MVP options.
- **Founder gate G0:** approve platform, scope, and whether the shield can ship.

## Milestone 1 — Product UX / design system
- Confirm experience map, screen inventory and light/dark visual direction.
- Define tokens/components; implement static polished shell.
- Test basic navigation with nontechnical users.
- **Founder gate G1:** approve visual quality and simplicity before large-scale build.

## Milestone 2 — Functional offline MVP
- Onboarding, commitments, tiny steps, focus timer, persistence, progress, settings.
- Automated tests, accessibility, offline recovery.
- **Founder gate G2:** confirm core behavior is useful without blocking or AI.

## Milestone 3 — Native focus integration (conditional)
- Add approved Shield/DeviceActivity integration and fallback UX.
- Test on real device, multiple iOS versions, permission and edge cases.
- **Founder gate G3:** confirm reliability or ship without blocker feature if needed.

## Milestone 4 — Private TestFlight and pilot
- Set up build/distribution pipeline, limited internal users and feedback capture.
- Pilot with consenting participants, review activation and meaningful-start behavior.
- **Founder gate G4:** approve iteration priorities and public launch criteria.

## Milestone 5 — Iteration and public release preparation
- Address usability/reliability gaps; app icon, naming, onboarding, listing, privacy policy, support.
- App Store entitlement and review compliance checks.
- Release only with explicit founder approval.

**No calendar estimates are promised by this PRD.** Engineering should propose effort estimates and dependencies after P0, not make guesses before proof.

---

# 11. Quality assurance, research, and user testing

## 11.1 Automated test strategy
- Unit: domain states, next-step fallback rules, daily grouping/timezones, progress aggregation.
- Integration: persistence, focus controller, extension event handling and error surfaces.
- React Native UI: navigation, form validation, modal close/back, empty states.
- Native: entitlement, actual shield on/off, app selection, revoked authorization, restarting, background schedules.
- Visual regression/screenshot review for key screens light/dark and text scaling.
- CI: formatting, lint, TypeScript check, unit/integration and build checks; no CI secrets echoed.

## 11.2 Manual device test matrix
- At least one current physical iPhone and latest supported iOS, plus another supported OS version/device if available.
- Screen Time enabled/disabled/denied/revoked.
- No selected apps, one app, several apps, selected category.
- Focus start/end, break, notification denied, screen lock/background/reboot.
- App force-quit, OS interruption and recovery.
- Light/dark; small/large accessibility text, VoiceOver, Reduce Motion.
- Low connectivity/offline; timezone change, midnight, DST transition.

## 11.3 Research plan
- Founding user + 10-20 adults from target group, with consent.
- Start with interviews about real avoidance moments, not hypothetical feature preferences.
- Observe whether they can get from opening app to starting a task with minimal instructions.
- Track 2-week experience with opt-in metrics and a lightweight debrief.
- Ask what they would miss if app disappeared; avoid leading questions.
- Use findings to rank P2, not to build everything on wishlists.

---

# 12. AI-assisted delivery operating model (ChatGPT + Claude Code + founder)

## 12.1 Roles and decision rights
- **Founder:** ultimate product owner/client; approves vision, major product changes, paid services, credentials, security-sensitive permissions, public releases, and milestone acceptance.
- **ChatGPT (interactive):** product manager/UX lead; maintains PRD, clarifies requirements, ranks backlog, reviews UX and product acceptance. ChatGPT in this chat is NOT a permanently running daemon.
- **Claude Code:** architecture/implementation lead; creates evidence-based ADRs, coding plans, tests, code and pull requests; challenges infeasible assumptions.
- **CI and optional OpenAI-powered automations/Codex review:** only after explicitly configured and funded; operate with scoped GitHub permissions. An OpenAI agent running via API is distinct from the interactive ChatGPT session.

## 12.2 Shared work artifacts
Recommended repo:
```
/
  README.md
  PRODUCT_REQUIREMENTS.md       # this file
  CLAUDE.md                    # agent instructions; must defer to this PRD
  docs/
    design/                    # design tokens, flows, screenshots
    architecture/              # ADRs and native findings
    feasibility/               # P0 report and device evidence
    decisions.md               # product tradeoffs with dates/approvals
    test-plan.md
  app/                         # app project, if architecture accepts RN
  ios/                         # generated or native modules/targets as chosen
  .github/
    ISSUE_TEMPLATE/
    PULL_REQUEST_TEMPLATE.md
    workflows/
```
If architecture chooses another project structure, record an ADR first.

## 12.3 Issue / PR loop
1. Approved feature is specified with user story, constraints, UX reference, acceptance criteria, dependency, and test plan.
2. Claude Code creates a branch, implements only approved scope, tests and opens a PR.
3. CI and independent reviews check correctness, privacy, accessibility, performance, and consistency with PRD.
4. Claude Code fixes actionable review issues with a bounded retry count (initially max two automatic passes).
5. Unresolved ambiguity/architectural change escalates to founder instead of guessing.
6. Required reviewer/founder approves merge at designated gates; release always human-approved.

## 12.4 Autonomy policy
**May automate:** routine issue implementation in approved scope, read-only research, tests, build checks, docs updates, PR creation, safe minor bug fixes.

**Require human approval:** expenses or subscriptions; sharing secrets; adding analytics/collecting sensitive data; changing privacy/data retention; new native permissions; major architecture shift; deleting repositories/branches/data; force pushes; disabling CI; merging to protected main if release-critical; sending user communications; TestFlight external release or App Store submission.

**Safety rails:**
- Private repository, protected main, PRs required for merge.
- Least-privilege short-lived GitHub/API credentials, no PAT in prompt or source.
- No cascading autonomous agents triggering one another indefinitely.
- Explicit cycle/time/cost ceilings and failure escalation.
- All tool actions and decisions traceable in issues/PRs.
- Never commit screenshots containing private user data; use synthetic fixtures.
- Human can pause automation immediately.
- No auto-accepting AI review comments if they conflict with PRD or security constraints.

## 12.5 Working cadence
- Weekly or milestone-based summary: shipped items, visual previews, failed tests, blockers, decisions needed, next priorities.
- Founder only needs to review significant product milestones and beta builds, not each line of code.
- No assumption that interactive ChatGPT and Claude Code are automatically in continuous conversation. GitHub and configured external agents provide the actual handoff.

---

# 13. Risks, dependencies and mitigations

| Risk | Severity | Mitigation / decision |
|---|---|---|
| Apple's Family Controls distribution entitlement denied/delayed | High | Request early; action-first offline app must work without shields. |
| Shield actions cannot implement imagined custom flow | High | P0 real-device test; use only documented actions and app-based fallback. |
| App extension/background scheduling unreliable | High | Isolate native adapter, persist state, test real iPhone and disclose limits. |
| App Review Guideline 4.10 monetization | High | Do not monetize built-in Screen Time APIs; review any future pricing with counsel/App Review guidance. |
| Users think "I failed" | High | Supportive copy, flexible goals, no broken streak penalties. |
| Visual design becomes cluttered | High | Design gate, one primary action per screen, max three tabs/commitments. |
| AI agents overbuild scope | High | PRD as source, gated issues, protected branches, explicit no-scope-creep rule. |
| Privacy exposure via selected apps/task text | High | Local-first, opaque tokens, redacted logs, minimal analytics. |
| Timer/blocks persist unexpectedly | High | Reliable recovery, visible state, force-unblock action, native tests. |
| User retention low | Medium | Pilot and interview; optimize moment of starting rather than gamification. |
| API/model/service cost | Medium | No AI backend in MVP, caps and explicit approval for new services. |
| Product name conflicts with existing brands | Medium | Working codename only; trademark/App Store/domain checks before brand selection. |

---

# 14. Open decisions / assumptions — do NOT treat as silently approved

1. **Final brand name** and app icon: TBD; "NextStep" is a working codename only.
2. **Stack:** React Native/Expo + Swift is default hypothesis; await P0 architecture ADR.
3. **Minimum iOS version:** Proposed iOS 18+ or a version justified by current SDK and intended audience; Claude must recommend target based on verified API availability and device support. Don't silently hardcode an unvalidated version.
4. **Screen Time experience:** Must verify distribution eligibility, shield customization, shield actions, availability, break/override scheduling.
5. **Task details:** Priority and optional saved backlog only if they don't harm simplicity.
6. **Notifications:** Optional and off until their user value is validated.
7. **Cloud/AI:** Phase 2 only; choose model/provider, cost controls, retention policies after validation.
8. **Commercial pricing:** TBD and constrained by Apple rule 4.10.
9. **Final visual tokens:** Founder to choose after seeing polished examples; suggested colors are provisional.
10. **Public product claims:** No health/clinical effectiveness claims without supporting research and appropriate review.

**Default interpretation:** When ambiguous, choose a safe, reversible, simple MVP implementation and ask at the next approval gate. Do not interpret this document as permission to invent entire sub-products.

---

# 15. Immediate instructions to Claude Code (the first execution request)

**Phase 0 is a feasibility and planning engagement, not full-scale app development.**

1. Read this PRD fully and restate the core user value and MVP scope in under 15 bullet points.
2. Create a short `docs/decisions.md` register of assumptions, recommended defaults and decision gates.
3. Research current Apple Screen Time APIs and App Store rules from official Apple documentation; verify exact supported APIs and OS/entitlement restrictions.
4. Propose two architecture options: React Native/Expo+Swift vs SwiftUI; recommend one with rationale, tradeoffs, maintenance implications and constraints.
5. Build the smallest possible local P0 proof-of-concept that can test app selection -> authorization -> shield -> unshield on a real iPhone. Do not claim it passed without real-device evidence supplied by the founder/tester.
6. Document distribution entitlement prerequisites for the main app and each extension and which founder actions are required.
7. Create `docs/feasibility/REPORT.md` recording commands, actual outcomes, OS/device, screenshots and open blockers. Mark untested items honestly.
8. After proof, propose the first polished design deliverables and a *short* milestone backlog.
9. Stop at approval Gate G0 before building the full MVP or purchasing/connecting services.
10. Never implement a generic dashboard UI in place of the premium minimal action-first experience defined here.

## First demo we want to see
- A device build (if Apple signing permits) that can request permission, select one distracting app, start a test focus period, show an Apple-approved custom shield when opening that app, and remove shield on end — **or** a clear reproducible evidence-backed explanation of which part is unavailable.
- A separate simple static design preview for Today screen showing the calm, premium art direction; no time spent on backend or AI coach yet.

---

# 16. Official references (recheck at implementation time)

These are starting references, not guarantees. Use currently released SDK docs and confirm with actual builds.

1. Apple — Request Family Controls entitlement: https://developer.apple.com/documentation/FamilyControls/requesting-the-family-controls-entitlement
2. Apple — Configure Family Controls in Xcode: https://developer.apple.com/documentation/xcode/configuring-family-controls
3. Apple — Family Controls, authorization: https://developer.apple.com/documentation/familycontrols
4. Apple — FamilyActivitySelection opaque tokens: https://developer.apple.com/documentation/familycontrols/familyactivityselection
5. Apple — Managed Settings UI / Shield Configuration: https://developer.apple.com/documentation/ManagedSettingsUI
6. Apple — Device Activity scheduling: https://developer.apple.com/documentation/deviceactivity/deviceactivityschedule
7. Apple — ShieldActionResponse (API availability including `openParentalControlsApp` must be tested): https://developer.apple.com/documentation/managedsettings/shieldactionresponse
8. Apple — App Review Guidelines, especially 4.10 monetizing built-in capabilities and 5.1 privacy: https://developer.apple.com/app-store/review/guidelines/
9. Apple — Human Interface Guidelines accessibility: https://developer.apple.com/design/human-interface-guidelines/accessibility
10. Expo — iOS app extensions: https://docs.expo.dev/build-reference/app-extensions/
11. Expo — custom native code: https://docs.expo.dev/workflow/customizing/
12. Expo — native development builds: https://docs.expo.dev/develop/development-builds/introduction/
13. Claude Code — cloud sessions and GitHub workflow: https://code.claude.com/docs/en/claude-code-on-the-web

---

# 17. Product quality bar: final checklist for founder acceptance

The MVP is **not** done merely because it compiles.

- [ ] First-time user immediately understands what to do.
- [ ] No required login to try the core product.
- [ ] User sees one compelling next action, not a complex task manager.
- [ ] Creating a commitment feels quick and rewarding.
- [ ] A short session can begin in one tap.
- [ ] App works without Screen Time permission; shield remains optional.
- [ ] If shield is present, it works reliably, doesn't trap users, and follows Apple rules.
- [ ] Starts and completed tasks are not conflated.
- [ ] Progress is reassuring, truthful, and not overwhelming.
- [ ] Light and dark modes feel intentional and premium.
- [ ] UI is consistent, polished, uncluttered, with refined motion and haptics.
- [ ] VoiceOver, large fonts, Reduced Motion and device interruptions are handled.
- [ ] The app respects users' privacy and permits full data deletion.
- [ ] No manipulative guilt, fake urgency, or addictive retention tricks.
- [ ] Native build and deployment workflow is reproducible.
- [ ] Founder has actually used the TestFlight build and approved the milestone.

**Ultimate standard:** The product should make a person say: *"This is so simple. I actually want to use it — and it helps me put my phone down and do what matters."*
