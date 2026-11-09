# BUG-006 After signing out of "Test login", all meetups disappear on the next sign-in

| Field | Value |
|---|---|
| **ID** | BUG-006 |
| **Type** | Functional – data persistence |
| **Severity** | Medium |
| **Priority** | P3 |
| **Status** | Won't fix (by design, development-only feature) – workaround documented |
| **Component** | Mobile app → Sign-in ("Test girişi" button) |
| **Reported** | 2026-11-01 |
| **Reporter** | Mukhtar Zakariyayev |

## Environment
- iPhone, iOS 18, Expo Go (development mode only; the button is not shown in store builds)

## Steps to reproduce
1. Sign in with **Test girişi (Test login)**.
2. Create a meetup.
3. Settings → **Sign out**.
4. Sign in again with **Test login**.
5. Open **My meetups**.

## Expected result
(Tester's expectation) The previously created meetup is still there.

## Actual result
The list is empty; the meetup is gone.

## Root cause
"Test login" uses anonymous authentication: every sign-in creates a brand-new anonymous account. After sign-out the previous anonymous account cannot be signed into again, so its data is unreachable (it still exists in the database).

## Resolution
- Data was moved to the tester's new account manually so testing could continue.
- Kept as is: the feature exists only for development and is removed before store release.
- Testers were instructed to use **Sign in with Apple / Google** when a persistent account is needed.

## Recommendation
Add a warning to the sign-out dialog when the account is anonymous ("Your test data will be lost"), or remove "Test login" entirely before the first store build.
