# Regression checklist — Hara?

Run before every store release (and the relevant section after each fix). Use **two accounts**: A = creator, B = participant. Mark ✅ / ❌ and the build number.

## Sign-in & profile
- [ ] Sign in with Apple → profile setup → home
- [ ] Sign in with Google (test user) → returns to the app, not to a browser error (BUG-008)
- [ ] Phone: send code, wrong code, correct code, resend (BUG-009, after Twilio upgrade)
- [ ] Profile: birth date under 18 is rejected; phone from phone sign-in is prefilled and locked
- [ ] Sign out → sign in again with the same method → data is still there (BUG-006)
- [ ] "Test login" is **not** visible in the store build

## Meetups & voting
- [ ] A creates a meetup (days, times, places; suggested + "All restaurants")
- [ ] B joins by code and by invite link; Couple / New date modes reject a 3rd member
- [ ] Votes update live on both phones
- [ ] B does **not** see "Reserve the winner" (BUG-001) or the invite box (BUG-003)
- [ ] Joined meetup appears in B's My meetups with "{A} invited you" (BUG-002)

## Reservations
- [ ] A sends a reservation; restaurant staff sees it in the panel
- [ ] Staff confirms / declines / proposes another time → both phones update and get a notification
- [ ] A accepts the alternative time; A cancels a reservation

## Notifications
- [ ] Push arrives for: join, leave, removed, reservation events, meetup deleted
- [ ] Tapping a push opens the right meetup; bell badge counts unread; opening the inbox clears it

## Safety (App Store)
- [ ] B reports A / the meetup → report appears in Admin → Reports
- [ ] Admin: close report, delete meetup, delete user — each gives feedback (BUG-007)
- [ ] A removes B → B loses access and gets "You were removed" (ENH-009)
- [ ] A blocks B → B removed, cannot rejoin, A gets no notifications about B
- [ ] B leaves a meetup → A notified; creator cannot leave
- [ ] A deletes a meetup → blocked while a reservation is active; otherwise B notified (ENH-008)
- [ ] Delete account → all data gone, sign-in starts fresh
- [ ] Privacy policy and Terms open **without login**, in the app language (BUG-005)

## Restaurants
- [ ] ⓘ opens details from voting, create screen and reservation card
- [ ] Gallery swipes; menu viewer: ✕ closes (BUG-010), ‹ › and thumbnails work, pinch-zoom
- [ ] "Open in Maps" uses the admin map link when set; "Call" opens the dialer
- [ ] Catalogue filters: district, metro, price, rating, mode fit, search, clear
- [ ] Admin: add / edit / delete restaurant (BUG-013), upload / reorder / delete photos, Save is last (BUG-012)

## Localisation & theme
- [ ] Switch AZ → EN → RU: no untranslated text on any screen above, push text in the chosen language
- [ ] Light / dark / system theme on every screen above; full-screen viewer readable

## Devices / layout
- [ ] Notch / Dynamic Island device: all top-bar buttons tappable in modals (BUG-010)
- [ ] Small screen (iPhone SE): no clipped buttons on create / voting / venue screens
