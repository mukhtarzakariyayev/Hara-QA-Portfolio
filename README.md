# Hara? — QA case study

Manual QA of a real product from the first build to App Store readiness: an iOS app for group meetups with restaurant reservations, plus a web admin / restaurant panel.

**Role:** QA tester and product owner — Mukhtar Zakariyayev
**Period:** 25 Oct – 9 Nov 2026
**Development:** code written by an AI coding assistant; every feature was handed to QA for testing on a real device before merge.

## What I tested
- **Mobile app (iOS, React Native / Expo):** sign-in (Apple, Google, SMS), profile, meetup creation, invite by code / link, live group voting, restaurant reservation, push notifications and inbox, report / block / remove member, account deletion, restaurant catalogue with filters, photo gallery and menu viewer, 3 languages (AZ / EN / RU), light / dark theme.
- **Web panel (Next.js):** admin statistics, restaurant management with photo upload, restaurant staff accounts, report moderation, public privacy policy & terms.
- **Backend behaviour (Supabase):** permissions between creator, participant, blocked user, restaurant staff and admin.

Details: [Test plan](test-plan.md) · [Regression checklist](regression-checklist.md) · [Enhancement requests](enhancements.md) · [Bug report template](templates/bug-report-template.md)

## Findings summary
| ID | Title | Type | Severity | Status |
|---|---|---|---|---|
| [BUG-008](bug-reports/BUG-008-google-sign-in-redirects-to-localhost.md) | Google Sign-In ends on a "can't connect" localhost page | Authentication | Critical | Fixed |
| [SEC-001](bug-reports/SEC-001-secret-key-exposed-in-screenshot.md) | Backend secret key exposed in a screenshot and stored as plaintext | Security | Critical | Fixed (key rotated) |
| [BUG-001](bug-reports/BUG-001-non-creator-sees-reserve-button.md) | Participant sees "Reserve the winner" | Permissions | High | Fixed |
| [BUG-005](bug-reports/BUG-005-legal-pages-redirect-to-admin-login.md) | Privacy policy / Terms open the admin login page | Release / compliance | High | Fixed |
| [BUG-007](bug-reports/BUG-007-admin-delete-meetup-button-does-nothing.md) | Admin "Delete meetup" button does nothing | Functional | High | Fixed |
| [BUG-009](bug-reports/BUG-009-sms-code-not-sent.md) | Phone sign-in: SMS not sent | Third-party config | High | Deferred |
| [BUG-010](bug-reports/BUG-010-menu-viewer-close-button-unresponsive.md) | Menu viewer ✕ unresponsive — user stuck | UI | High | Fixed |
| [BUG-002](bug-reports/BUG-002-joined-meetups-missing-from-my-meetups.md) | Joined meetups missing from My meetups | Functional | Medium | Fixed |
| [BUG-003](bug-reports/BUG-003-participant-can-share-invite-code.md) | Participant can share the invite code | Permissions | Medium | Fixed |
| [BUG-004](bug-reports/BUG-004-redundant-manual-participant-names.md) | Redundant manual participant names | Requirement | Medium | Fixed |
| [BUG-006](bug-reports/BUG-006-test-login-data-lost-after-sign-out.md) | Test login loses data after sign-out | Data | Medium | Won't fix (dev-only) |
| [BUG-013](bug-reports/BUG-013-admin-cannot-delete-restaurant.md) | Restaurants cannot be deleted | Missing function | Medium | Fixed |
| [BUG-011](bug-reports/BUG-011-menu-viewer-design-too-plain.md) | Menu viewer not book-like, no page navigation | UX | Low | Fixed |
| [BUG-012](bug-reports/BUG-012-venue-form-save-button-position.md) | Save button in the middle of the admin form | UX | Low | Fixed |
| [DOC-001](bug-reports/DOC-001-google-oauth-setup-guide-inaccurate.md) | Google setup guide didn't match the console | Documentation | Low | Fixed |
| [ENV-001](bug-reports/ENV-001-app-does-not-open-dev-server-stopped.md) | App doesn't open — dev server stopped | Environment | — | Not a bug |
| [ENV-002](bug-reports/ENV-002-new-option-missing-stale-bundle.md) | New option missing — stale build on device | Environment | — | Not a bug |

**Totals:** 13 bugs, 1 security issue, 1 documentation issue, 2 environment triage cases, 9 enhancement requests.

## How the reports are written
Each report follows the [template](templates/bug-report-template.md): environment, preconditions, numbered steps, expected vs actual, frequency, evidence, then root cause, fix and retest result. Root-cause notes come from the developer; reproduction, expected behaviour, triage and verification are mine. Personal data (phone numbers, e-mails, keys, user IDs) has been removed.

## Skills shown
- Writing reproducible bug reports with clear expected / actual results
- Severity & priority assessment; separating product bugs from environment and third-party issues
- Permission testing with multiple roles (creator, participant, blocked user, staff, admin)
- Retesting fixes and thinking about regressions; turning findings into a regression checklist
- Spotting requirement and UX problems, not only crashes
- Security awareness (secret handling, key rotation)

---

### Azərbaycanca qısa
Bu repo **Hara?** tətbiqinin (görüş planlaşdırma + restoran rezervasiyası) ilk versiyadan App Store-a hazırlığa qədər QA prosesini göstərir. Bütün funksiyaları real iPhone-da sınamışam, tapdığım buglar üçün addım-addım reportlar yazılıb, hər birinin kök səbəbi, düzəlişi və yenidən yoxlanması qeyd olunub. Əlavə olaraq test planı və buraxılışdan əvvəl istifadə olunan regression checklist var.
