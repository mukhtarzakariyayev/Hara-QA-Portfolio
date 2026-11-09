# BUG-002 Meetups joined by invite code are missing from "My meetups"

| Field | Value |
|---|---|
| **ID** | BUG-002 |
| **Type** | Functional |
| **Severity** | Medium |
| **Priority** | P2 |
| **Status** | Fixed – Verified |
| **Component** | Mobile app → "Görüşlərim" (My meetups) tab |
| **Reported** | 2026-10-26 |
| **Reporter** | Mukhtar Zakariyayev |
| **Fixed in** | PR #5 (`feat/my-meetups`) |

## Environment
- iPhone, iOS 18, Expo Go
- Two accounts: creator and participant

## Preconditions
User B has joined User A's meetup using the invite code.

## Steps to reproduce
1. Log in as User B.
2. Open the **Görüşlərim** tab.

## Expected result
The list shows every meetup the user belongs to — the ones they created **and** the ones they joined — with a label "{name} invited you" for joined ones, so the participant can return to vote later.

## Actual result
Only meetups created by the user are listed. After closing the voting screen, a participant has no way to get back to a joined meetup except re-entering the code.

## Frequency
Always

## Root cause
The list query filtered by `created_by = current user` instead of membership.

## Fix
The query now selects meetups through `meetup_members` and shows the creator's name for joined meetups ("{name} dəvət edib").

## Verification
2026-10-26 — tester created a meetup, the developer joined with a test account and vice versa; both meetups appear with the correct labels. ✅
