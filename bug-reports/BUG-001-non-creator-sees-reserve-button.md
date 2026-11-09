# BUG-001 Participant who joined by invite code sees "Reserve the winner" button

| Field | Value |
|---|---|
| **ID** | BUG-001 |
| **Type** | Functional – permissions |
| **Severity** | High |
| **Priority** | P1 |
| **Status** | Fixed – Verified |
| **Component** | Mobile app → Voting screen |
| **Reported** | 2026-10-26 |
| **Reporter** | Mukhtar Zakariyayev |
| **Fixed in** | PR #5 (`feat/my-meetups`) |

## Environment
- iPhone, iOS 18, Expo Go (development build of the app)
- Backend: Supabase (test project), two accounts: meetup creator and invited participant

## Preconditions
- User A has created a meetup.
- User B has joined the meetup with the invite code.

## Steps to reproduce
1. Log in as User B.
2. Open the meetup User A created.
3. Vote in every section (day, time, place).
4. Look at the button at the bottom of the screen.

## Expected result
Only the meetup creator can send a reservation request to the restaurant. Participants see a note such as "Your vote is saved. The reservation will be made by {creator}".

## Actual result
User B sees and can tap **"Qalibi rezerv et" (Reserve the winner)**, i.e. a participant can start a reservation for a meetup they do not own.

## Frequency
Always

## Root cause
The footer button was rendered for every member; the screen did not check whether the current user is the meetup creator.

## Fix
The footer now shows the reservation button only when `meetup.created_by === currentUser`. Other members see an informational note with the creator's name. The database rule (RLS) also allows only the creator to insert a reservation.

## Verification
2026-10-26 — retested on iPhone with two accounts: creator sees the button, participant sees the note. ✅
