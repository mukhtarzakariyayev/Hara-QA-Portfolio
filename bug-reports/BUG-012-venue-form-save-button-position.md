# BUG-012 Admin restaurant form: "Save" button is above the photo section, so the form looks finished too early

| Field | Value |
|---|---|
| **ID** | BUG-012 |
| **Type** | UX |
| **Severity** | Low |
| **Priority** | P3 |
| **Status** | Fixed – Verified |
| **Component** | Web admin panel → Restaurants → Edit restaurant |
| **Reported** | 2026-11-09 |
| **Reporter** | Mukhtar Zakariyayev |

## Environment
- Windows 11, Chromium-based browser, production admin panel

## Steps to reproduce
1. Admin → **Restoranlar** → open any restaurant.
2. Scroll through the page.

## Expected result
All inputs that describe the restaurant (details, district/metro, map link, modes, price, photos, active flag) come first; the **Yadda saxla (Save)** button is the last element of the form.

## Actual result
The **Save** button sits in the middle of the page; the photo section and other blocks follow it. Admins may click Save and leave before uploading photos, or think the photo section is unrelated to the restaurant.

## Resolution
The photo section was moved inside the form, above the **Active** checkbox; **Save** is now the last element. A note explains that photos upload immediately when selected.

## Verification
2026-11-09 — order is details → location → modes/price → photos → active → Save. ✅
