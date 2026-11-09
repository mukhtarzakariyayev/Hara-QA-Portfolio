# BUG-005 "Privacy policy" and "Terms of use" links open the admin login page instead of the documents

| Field | Value |
|---|---|
| **ID** | BUG-005 |
| **Type** | Functional / release (App Store compliance) |
| **Severity** | High |
| **Priority** | P1 |
| **Status** | Fixed – Verified |
| **Component** | Mobile app → Settings; Web panel → public pages |
| **Reported** | 2026-11-01 |
| **Reporter** | Mukhtar Zakariyayev |

## Environment
- iPhone, iOS 18, Expo Go
- Production web panel on Vercel

## Preconditions
User is logged in to the mobile app (not to the admin panel).

## Steps to reproduce
1. Mobile app → **Ayarlar (Settings)**.
2. Tap **Məxfilik siyasəti (Privacy policy)** or **İstifadə şərtləri (Terms of use)**.

## Expected result
The document opens in the in-app browser, in the app's language, without any login. (Apple requires a publicly reachable privacy policy URL.)

## Actual result
The browser opens the **admin / restaurant panel login page**. Regular users cannot read the documents.

## Frequency
Always

## Root cause
The new public pages and the change that exempts `/privacy` and `/terms` from the login redirect existed only locally; the production panel was still the old deployment, where every unauthenticated request is redirected to `/login`.

## Fix
Deployed the panel version with the public paths (`/login`, `/privacy`, `/terms`) excluded from the authentication redirect.

## Verification
2026-11-01 — `/privacy?lang=az` and `/terms?lang=en` return the documents without login; `/admin/reports` still redirects to login (no regression in access control). ✅

## Note for process
Mobile features that depend on the web panel must be released together with the panel deployment; add "linked web pages reachable without login" to the release checklist.
