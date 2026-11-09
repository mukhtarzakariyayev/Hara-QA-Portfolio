# BUG-009 Phone sign-in: "SMS was not sent" error on "Send code"

| Field | Value |
|---|---|
| **ID** | BUG-009 |
| **Type** | Configuration / third-party integration |
| **Severity** | High |
| **Priority** | P2 |
| **Status** | Deferred – blocked by third-party account plan |
| **Component** | Mobile app → Sign-in → Phone number; SMS provider (Twilio Verify) |
| **Reported** | 2026-11-02 |
| **Reporter** | Mukhtar Zakariyayev |

## Environment
- iPhone, iOS 18, Expo Go
- Supabase phone auth with Twilio Verify, Twilio **trial** account

## Steps to reproduce
1. Sign-in screen → **Telefon nömrəsi ilə davam et (Continue with phone number)**.
2. Enter a valid Azerbaijani mobile number (+994 …).
3. Tap **Kodu göndər (Send code)**.

## Expected result
A 6-digit code arrives by SMS and the code entry screen opens.

## Actual result
Red error under the field: "SMS göndərilmədi. Nömrəni yoxla və ya bir az sonra cəhd et." (SMS was not sent. Check the number or try again later.) No SMS arrives.

## Investigation (auth logs)
- Attempt with the tester's verified number: `Invalid template name. Trial accounts can only use predefined SMS templates` (Twilio error 572006).
- Attempt with a mistyped number: `No Twilio trial phone number is assigned for messaging to this destination number` (572002) — trial accounts can send only to verified numbers.

## Root cause
Limitations of the SMS provider's free trial: custom message templates and unverified recipients are not allowed. The application code works as intended.

## Resolution plan
Upgrade the Twilio account to a paid plan; no code change needed. Retest the full phone flow (send, wrong code, expired code, resend) after the upgrade.

## Side finding
The app shows the same generic error for every failure. Suggest distinguishing "invalid number" from "service unavailable" to help users and support.
