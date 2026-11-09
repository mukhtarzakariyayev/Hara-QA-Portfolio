# BUG-004 Creator must type participant names manually although participants join by code

| Field | Value |
|---|---|
| **ID** | BUG-004 |
| **Type** | Requirement / design defect |
| **Severity** | Medium |
| **Priority** | P2 |
| **Status** | Fixed – Verified |
| **Component** | Mobile app → Create meetup screen |
| **Reported** | 2026-10-26 |
| **Reporter** | Mukhtar Zakariyayev |
| **Fixed in** | PR #4 (`feat/expected-count`) |

## Description
The "Create meetup" screen asked the creator to type every participant's name. Participants then joined with the invite code under their own profile names, so the typed names were never used, could differ from real names and doubled the work.

## Steps to reproduce
1. Open **Create meetup**.
2. Fill in the participant names.
3. Share the invite code; let a friend join.
4. Compare the voting screen's member list with the typed names.

## Expected result
The creator should not enter data that the system gets anyway. Only information that is really needed (approximate party size for the restaurant) should be asked.

## Actual result
Typed names are ignored; members appear under their profile names. The form step is redundant and confusing.

## Resolution
Removed the names field. The creator now sets the **expected number of people** (needed for the reservation party size). Two-person modes (Couple, New date) are fixed at 2. The voting screen shows "Joined (x/y)".

## Verification
2026-10-26 — created a meetup with an expected count of 2, developer joined with the invite code; screen showed "1/2 voted · Joined (2/2)" with both names. ✅
