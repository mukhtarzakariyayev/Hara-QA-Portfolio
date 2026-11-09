# ENV-002 New "Remove from meetup" option not visible after the change was delivered

| Field | Value |
|---|---|
| **ID** | ENV-002 |
| **Type** | Test environment |
| **Severity** | — |
| **Status** | Not a bug – stale build on device |
| **Component** | Mobile app → Voting screen → member actions |
| **Reported** | 2026-11-09 |
| **Reporter** | Mukhtar Zakariyayev |

## Steps to reproduce
1. As the meetup creator, open a meetup with another member.
2. Tap the other member's name.

## Expected result (per new feature)
Actions: **Görüşdən çıxar (Remove from meetup)**, Report, Block, Cancel.

## Actual result
Only Report, Block, Cancel.

## Triage
- Code on the server contained the option; dev server was running.
- Database confirmed the tester's account is the creator of the meetup (so the role check would pass).
- Conclusion: the phone was still running the previously loaded JavaScript bundle.

## Resolution
Reloading the app in Expo Go (shake → Reload, or force-close and reopen) showed the option; the feature was then verified end-to-end (removed member received the notification).

## Process improvement
Before verifying a fix, always reload / reinstall the build and note the build or commit in the test result.
