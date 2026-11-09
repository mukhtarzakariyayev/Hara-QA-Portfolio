# ENV-001 App cannot be opened on the iPhone ("could not connect")

| Field | Value |
|---|---|
| **ID** | ENV-001 |
| **Type** | Test environment |
| **Severity** | — (blocker for testing only) |
| **Status** | Not a bug – environment |
| **Component** | Development environment (Expo dev server) |
| **Reported** | 2026-11-01 |
| **Reporter** | Mukhtar Zakariyayev |

## Steps to reproduce
1. Open Expo Go on the iPhone.
2. Tap the **Hara?** project.

## Actual result
The app does not load; Expo Go cannot reach the project.

## Triage
The development server on the developer's computer had stopped. The app itself was unchanged. Restarting the server fixed it immediately; the app bundled and opened on the phone.

## Why it is not a product bug
End users install store builds that do not depend on a developer's computer. The issue affects only the test setup.

## Process improvement
Before a test session, confirm the dev server is running (status page shows `packager-status:running`), or test on a cloud development / TestFlight build.
