# BUG-007 Admin panel → Reports: "Delete meetup" button does nothing

| Field | Value |
|---|---|
| **ID** | BUG-007 |
| **Type** | Functional |
| **Severity** | High |
| **Priority** | P1 |
| **Status** | Fixed – Verified |
| **Component** | Web admin panel → Şikayətlər (Reports) |
| **Reported** | 2026-11-01 |
| **Reporter** | Mukhtar Zakariyayev |

## Environment
- Windows 11, Chromium-based browser
- Production admin panel (Vercel)

## Preconditions
- Logged in as admin.
- There is an open report about a meetup.

## Steps to reproduce
1. Open **Admin → Şikayətlər**.
2. On an open report, click **Görüşü sil (Delete meetup)**.

## Expected result
A confirmation is shown; after confirming, the meetup is deleted and the report is marked **Closed**. If deletion fails, an error message explains why. (Apple requires that reported content can be removed within 24 hours.)

## Actual result
Nothing happens: no confirmation, no error. The report stays **Open** and the meetup still exists in the app.

## Frequency
Always (in the tester's browser)

## Investigation
- Database: the report was still open and the meetup existed → the delete request never reached the server.
- Server logs: no request recorded for the action.
- Deleting the meetup directly in the database worked (tested in a rolled-back transaction).

## Root cause
The button relied on the browser's native `window.confirm()` dialog. The dialog was blocked/suppressed in the tester's browser, so the click was cancelled silently. In addition, server-side errors were ignored, so even a failed delete would have shown no feedback.

## Fix
- Confirmation moved into the page itself: the button turns into "… delete? [Yes, delete] [Cancel]".
- Server action returns errors, which are shown under the button.
- Same fix applied to **Delete user**.

## Verification
2026-11-01 — on production: in-page confirmation appears, meetup is deleted, report becomes **Closed**. ✅
