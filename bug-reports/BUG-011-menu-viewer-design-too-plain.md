# BUG-011 Menu viewer looks unfinished; no sense of "pages", no way to jump between pages

| Field | Value |
|---|---|
| **ID** | BUG-011 |
| **Type** | UX / UI improvement |
| **Severity** | Low |
| **Priority** | P2 |
| **Status** | Fixed – Verified |
| **Component** | Mobile app → Restaurant details → Menu |
| **Reported** | 2026-11-09 |
| **Reporter** | Mukhtar Zakariyayev |

## Description
The requirement was a "book-like" menu. The first version showed plain photos on a black screen: no page feeling, no page controls, no overview of how many pages exist, and only one entry point ("View the menu") on the restaurant screen.

## Expected result
- Pages look like menu sheets and are turned like a book.
- The user can see all pages and jump to any of them.
- Current position is visible.

## Actual result
Plain full-bleed images; swipe was the only navigation; the page counter was hard to notice.

## Resolution
- Pages are shown as cream "paper" sheets with a soft shadow on a dark background.
- ‹ › page-turn buttons on both sides, swipe still works, pinch-to-zoom kept.
- Thumbnail strip at the bottom with the current page highlighted in gold; tap to jump.
- "2 / 5" counter pill in the top bar.
- Restaurant screen shows the pages as a row of numbered thumbnails; tapping one opens the viewer at that page.

## Verification
2026-11-09 — all navigation options work on iPhone; interior photos use the same viewer without the paper style. ✅
