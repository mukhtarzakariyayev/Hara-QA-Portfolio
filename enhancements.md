# Enhancement requests raised during testing

Gaps found while testing that were not defects in existing behaviour but missing functionality or poor UX. All were implemented and verified on device.

| ID | Request | Why (observed during testing) | Result |
|---|---|---|---|
| ENH-001 | Separate **My meetups** tab between Home and Settings | Meetups were only reachable from the screen right after creation | Bottom tab added |
| ENH-002 | Settings split into **Profile / Language / Appearance** pages; app in **AZ / EN / RU**; light & dark theme | One long settings page was hard to scan; target market is multilingual | Implemented |
| ENH-003 | **In-app notification inbox** with bell icon and unread badge | Push notifications disappeared once dismissed; no history | Bell + list + live unread count |
| ENH-004 | Restaurant **info (ⓘ) before voting** and on the create screen | Creator had to choose restaurants without seeing address/phone/photos | Restaurant details screen |
| ENH-005 | **All restaurants** catalogue with **filters** (district, nearby metro, average price, rating, mode fit) | Creator could pick only from a short suggested list | Catalogue + filters |
| ENH-006 | Structured **district / metro** fields and **Google Maps link** in the admin form | Free-text address made filters imprecise; "Open in Maps" searched by text | Dropdowns + map link |
| ENH-007 | **Interior photo gallery** and **menu pages** (book-like) | Users could not judge a restaurant from its name only | Gallery + menu viewer |
| ENH-008 | Creator can **delete a meetup**; participants are notified | Test meetups piled up; no way to clean up | Delete with confirmation; blocked while a reservation is active |
| ENH-009 | Creator can **remove a member** without blocking; removed member and others are notified | Only "block" existed; removed people silently lost access | Remove + `member_removed` / `member_left` notifications |
