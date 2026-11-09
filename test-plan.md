# Test plan — Hara? (MVP)

## 1. Product under test
**Hara?** is an iOS app (React Native / Expo) for small groups to vote on a day, time and place for a meetup and send a reservation request to a partner restaurant. A web admin & restaurant panel (Next.js) manages restaurants, reports and reservation responses. Backend: Supabase (Postgres with row-level security, realtime, storage, push notifications).

## 2. Scope
**In scope**
- Sign-in: Apple, Google, phone (SMS), test login (development only)
- Profile setup and editing (name, phone, city, birth date, gender, 18+)
- Meetup lifecycle: create, invite by code / link, join, vote (live updates), delete
- Reservations: request, restaurant response (confirm / decline / alternative time), accept alternative, cancel
- Notifications: push + in-app inbox (join, leave, remove, reservation events, meetup deleted)
- Safety (App Store requirements): report, block, remove member, leave meetup, delete account, privacy policy & terms
- Restaurants: details screen, gallery, menu viewer, catalogue & filters, map / call
- Localisation (AZ / EN / RU) and light / dark theme
- Web panel: admin statistics, restaurant CRUD and photos, staff accounts, reports moderation; restaurant staff reservation list

**Out of scope (this phase)**
- Android, performance / load testing, automated UI tests, payment

## 3. Approach
- **Manual exploratory and scenario testing** on a real iPhone (Expo Go) after every feature, as the end user would use it.
- **Multi-user scenarios** with a second test account (creator vs participant, blocked user, restaurant staff).
- **Retest + regression** of related areas after each fix (e.g. permissions on all creator-only actions).
- Developer-side checks before handing over a build: type check, lint, database rule checks with test accounts (REST calls).

## 4. Environments
| Layer | Environment |
|---|---|
| Mobile | iPhone, iOS 18, Expo Go (SDK 58) |
| Web panel | Production on Vercel; Windows 11, Chromium-based browser |
| Backend | Supabase project (EU-Frankfurt), free plan |
| Test data | Demo restaurants (flagged "Nümunə"), temporary anonymous test accounts deleted after each session |

## 5. Entry / exit criteria
- **Entry:** feature merged to a branch, dev server running, build reloaded on the device (see ENV-002).
- **Exit (per feature):** all scenarios pass on device, no open Critical/High defects, related regression items pass.
- **Exit (store release):** full [regression checklist](regression-checklist.md) passes on a TestFlight build.

## 6. Severity scale
| Severity | Meaning | Example |
|---|---|---|
| Critical | Blocks a core flow or exposes data; no workaround | BUG-008 Google sign-in, SEC-001 |
| High | Core feature broken or wrong permissions; workaround is poor | BUG-001, BUG-007, BUG-010 |
| Medium | Feature partly broken or missing; workaround exists | BUG-002, BUG-013 |
| Low | Cosmetic / UX / documentation | BUG-011, BUG-012, DOC-001 |

## 7. Risks
- Third-party consoles (Apple, Google, Twilio, Vercel) change often → setup guides go stale (DOC-001).
- Free-plan backend pauses after a week of inactivity → first test of the day may fail.
- Expo Go differs from store builds (redirect URLs, push on Android) → final pass must run on TestFlight.
