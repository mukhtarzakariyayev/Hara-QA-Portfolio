# SEC-001 Backend secret key exposed in a shared screenshot and stored as readable plaintext

| Field | Value |
|---|---|
| **ID** | SEC-001 |
| **Type** | Security / configuration |
| **Severity** | Critical |
| **Priority** | P1 |
| **Status** | Fixed – Verified |
| **Component** | Web admin panel → Vercel environment variables |
| **Reported** | 2026-11-01 |
| **Reporter** | Mukhtar Zakariyayev (self-reported during setup) |

## Description
While configuring the production admin panel on Vercel, a screenshot of the environment-variables screen was shared in a chat. The screenshot showed the full value of the **Supabase secret (service-role) key**, which bypasses all database security rules. The variable was also saved with type **Plaintext**, so anyone with project access could read it. In the same session an existing variable (`NEXT_PUBLIC_SUPABASE_URL`) was accidentally renamed instead of creating a new one, which removed the database URL from the deployment.

## Steps to reproduce (how it happened)
1. Vercel → Project → Settings → Environment Variables.
2. Open an existing variable's edit form and type a new key name and the secret value.
3. Take a screenshot of the form and share it.

## Expected result
- Secret values are never shown in screenshots, tickets or chats.
- Secrets are stored as **Sensitive / Secret** (write-only) variables.
- Adding a variable never modifies an unrelated existing variable.

## Actual result
- The secret was visible in the shared image.
- It was stored as readable plaintext (Vercel flagged it as "readable-secret").
- The database URL variable was overwritten.

## Impact
Anyone who saw the image could read, change or delete all user data.

## Resolution
1. All variables were deleted and recreated from scratch; the URL variable was restored.
2. A **new** secret key was generated in Supabase and stored in Vercel as a **Sensitive** variable (value hidden after saving).
3. The exposed key was deleted in Supabase, so the leaked value no longer works.
4. Panel redeployed and verified.

## Verification
2026-11-01 — environment list shows the secret with a lock icon and no visible value; the admin login and staff management (which need the key) work. ✅

## Lessons learned
- Crop or blur secrets before sharing any screenshot.
- Rotate a key immediately once it has been exposed; deleting the image is not enough.
- Use the "Add new" form for new variables, not an existing variable's edit form.
