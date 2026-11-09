# BUG-010 Restaurant menu viewer: the ✕ (close) button does not respond — user is stuck in the viewer

| Field | Value |
|---|---|
| **ID** | BUG-010 |
| **Type** | Functional / UI |
| **Severity** | High |
| **Priority** | P1 |
| **Status** | Fixed – Verified |
| **Component** | Mobile app → Restaurant details → Menu (full-screen viewer) |
| **Reported** | 2026-11-09 |
| **Reporter** | Mukhtar Zakariyayev |

## Environment
- iPhone with Dynamic Island, iOS 18, Expo Go

## Preconditions
The restaurant has menu pages uploaded in the admin panel.

## Steps to reproduce
1. Open a meetup → tap ⓘ next to a restaurant.
2. Tap **Menyuya bax (View the menu)**.
3. Tap the ✕ button in the top-right corner.

## Expected result
The viewer closes and the restaurant screen is shown again.

## Actual result
Nothing happens. The viewer covers the whole screen and there is no other way back (no swipe-down), so the user has to restart the app.

## Frequency
Always

## Root cause
The viewer is a separate full-screen window. Its top bar was positioned at the very top of the screen, under the status bar / Dynamic Island area, where iOS intercepts touches.

## Fix
The top bar is now placed below the safe area (top inset), and the close button is larger (40 pt) with a visible background.

## Verification
2026-11-09 — ✕ closes the viewer for both menu pages and interior photos. ✅

## Regression note
Check every full-screen modal on notch / Dynamic Island devices: tappable elements must be inside the safe area.
