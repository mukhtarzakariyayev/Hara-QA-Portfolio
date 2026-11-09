# BUG-003 Participant (not creator) sees the "Invite friends" code box and can share the meetup

| Field | Value |
|---|---|
| **ID** | BUG-003 |
| **Type** | Functional – permissions |
| **Severity** | Medium |
| **Priority** | P2 |
| **Status** | Fixed – Verified |
| **Component** | Mobile app → Voting screen |
| **Reported** | 2026-10-26 |
| **Reporter** | Mukhtar Zakariyayev |
| **Fixed in** | PR #6 (`fix/invite-creator-only`) |

## Environment
- iPhone, iOS 18, Expo Go

## Preconditions
User B joined User A's meetup with the invite code.

## Steps to reproduce
1. Log in as User B.
2. Open the joined meetup.

## Expected result
Only the creator decides who is invited, so only the creator sees the "Dostlarını dəvət et · kod" box and the **Share** action.

## Actual result
The invite box with the code and the **Paylaş (Share)** button is visible to every participant, so anyone can forward the meetup to people the creator did not invite.

## Frequency
Always

## Root cause
The invite box had no role check (same root cause family as BUG-001).

## Fix
The invite box is rendered only for the creator. For two-person modes (Couple, New date) it is also hidden once the meetup is full.

## Verification
2026-10-26 — participant no longer sees the box; creator still does. ✅
