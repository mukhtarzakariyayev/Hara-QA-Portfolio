# BUG-013 Admin panel: restaurants can be added but not deleted

| Field | Value |
|---|---|
| **ID** | BUG-013 |
| **Type** | Functional – missing CRUD operation |
| **Severity** | Medium |
| **Priority** | P2 |
| **Status** | Fixed – Verified |
| **Component** | Web admin panel → Restaurants |
| **Reported** | 2026-11-09 |
| **Reporter** | Mukhtar Zakariyayev |

## Steps to reproduce
1. Admin → **Restoranlar** → open a restaurant (e.g. a demo venue).
2. Look for a way to remove it.

## Expected result
The admin can permanently delete a restaurant (with confirmation), e.g. to remove demo data or an ended partnership.

## Actual result
There is no delete option; only "Active" can be unchecked to hide it.

## Developer analysis
A restaurant with reservation requests cannot be deleted at database level (foreign key protects reservations), so a simple delete would fail for active partners.

## Resolution
- **Restoranı sil (Delete restaurant)** section at the bottom of the restaurant page with in-page confirmation; the question shows how many reservation requests will be deleted.
- Deletes photos (storage), reservation requests and staff links; staff panel accounts are kept.
- After deletion the admin returns to the list with a "… deleted" message.
- The page recommends unchecking **Active** for temporary hiding.

## Verification
2026-11-09 — demo restaurant deleted on production; it disappears from the panel list and from the app. ✅
