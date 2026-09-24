# Coordination log · Figma "Design flow"

File: https://www.figma.com/design/Ereat5qYENeSKTvW473gn5/Design-flow
Live board inside the file: page "Design system", section "Coordination · agents working on this file (read before editing)".

At least two AI sessions edited this file on 24 Sep 2026. Before editing:

1. Read the board in the file and add or update your own block.
2. Claim the frames or sections you will touch.
3. Never delete or rename a section you did not create. If a name collides, rename yours.
4. Guard every scripted edit: change a layer only if it still has the value you read.

## Session A · Claude Code (cloud) · session_01CfbgfhugfvbdN8DuxoRyyh

Status: finished, no longer editing the file.

### Design system (page "Design system")

- Tokens: collection renamed "Rentbutik · Tokens"; iOS code syntax and a description on every variable; new `radius/group` = 22.
- Prototype collection renamed "Prototype · Screen state (not design tokens)", mode "Default".
- Text styles: SwiftUI names fixed (`.largeTitle`, `.title`, `.caption`; weights as `.bold()` / `.weight(.semibold)`).
- Effect styles: SwiftUI shadow values (Figma blur 18 = SwiftUI radius 9).
- 04 Components: Label / Title / Subtitle / Value / Show… properties on Button / Large, Button / Small, Control / Slide, Chip / Hold countdown, List / Row, Tile / Bento, Status chip. Descriptions list props, SwiftUI API and the screens that use each one.
- Legacy components marked DEPRECATED: Vehicle badge, Notification row, Conversation row, Capture slot, Map step card.
- `Icon / pause.circle.fill` is now a real cut-out (the pause bars were invisible).
- 00 Guidelines: radius and spacing lines match the tokens.

### Screen fixes (Production flow and Dark mode page)

| Screen | Change |
|---|---|
| H04 | "This week" → "Past 2 weeks" (items are 12–18 Sep, today is 23 Sep) |
| H02 | Date "22 Sep 2026 at 10:02" → "23 Sep 2026 at 09:39" (variable `Notification/date`) |
| H01golf | Tile "18:05 ₼9.50" → "1:42 ₼38.00", same as G03 |
| C03 | "replies in about 5 min" → "usually replies in 5 min", same wording as C02 |
| T01b | Car rental current trip: Open trip hidden, Support full width (handoff notes: car rentals have no Open trip) |
| P01 | Notifications subtitle "Choose alerts" → "Push · Trip updates" (variable `Notification summary`) |
| A06c | Hold timer 29:41 → 25:12 |
| HO01–HO08, HO02b–d, HO04b, HO07a | Tab bar selects Profile, not Home; tint copied from P01 |
| HO04, HO04b | Button / Small was invisible on the screen background; now `surface/control` + controlShadow |
| Host / Car row | Paused icon shows its pause bars |
| R01g | Spec chip "2" → "2 seats" |
| EV01 | Tariff segment "₼0.25/min" no longer truncated; 4th segment layer renamed "Segment / Driver" |
| EV02 (7 frames) | Tray labels on one baseline; Inside thumbnail showed a white box, now the seat icon; Inside stage had two dashed outlines, now one |
| EV04 | "Sahil → 28 May" → "Sahil → 28 May street", same as T01b |
| G02 | Reservation card moved up 26 pt to clear the tab bar, like G01 |
| G03, G03c | "Golf cart 4 ·₼38.00" → "Golf cart 4 · ₼38.00" |
| TR02 | Pickup row icon shield.fill → mappin.and.ellipse; row sizing repaired |
| 12 · Handoff notes | Home module list = Transfer / Renter / Electric / Golf; 11 · Transfer rows rewritten for TR01–TR02 and HO06–HO08 (215 rows). HANDOFF-NOTES.md needs the same update |

## Session B · the agent that wrote "06 · SwiftUI build guide"

Seen from Session A: fixed HO07 "Car & driver", the Trips transfer icon, merged the two Dark mode copies into one, added EV plan and Places tiles to P01.

To settle:

1. Motion values in 06 differ from the shipping code. `Rentbutik/Design/Theme.swift` in Emin-dev/figma and `design/RULES.md` D: `Theme.smooth = .smooth(duration: 0.45)`, `Theme.snappy = .snappy(duration: 0.32, extraBounce: 0.02)`, `Theme.bouncy = .spring(response: 0.5, dampingFraction: 0.82)`. 06 says `.spring(duration: 0.45, bounce: 0)`, `.spring(duration: 0.32, bounce: 0.15)`, `.spring(duration: 0.40, bounce: 0.35)`.
2. Haptics in 06 differ from `design/RULES.md` E for gain, celebrate and ignition.

## Open decisions for Emin

1. Done: Host / Car row is a documented component set (State × 6, props Car / Status / Detail), moved to Production · 00 Reusable assets.
2. Production screens use their own layers, not instances of the 04 components. Swapping them is a separate job.
3. R01a Dates: the calendar highlights 28–30, the fields and R04 say 28–29 (1 day). Emin chose to fix the calendar. Session A added a hidden "Selected (show on range start / end)" layer to every day cell of the Date range calendar main component. New layers do not reach existing instances through the API, so finish it in the Figma app: in R01a show "Selected" on Day 29 (text on-gold, right corners 20) and clear Day 30 (no fill, circle fill none, text ink, Callout).
4. Done: TR01c Route sheet now shows the Baku → Airport ride (Production and Dark).
5. Done: W03 EV ride row uses bolt.car.fill (Production and Dark).

## Decisions

- 24 Sep 2026 · Dark mode background: keep Apple system black. Screen #000000, cards and sheets #1C1C1E, rows and controls inside sheets #2C2C2E. Soft neutral black (#0E0E10) and warm brand black (#110F0D) were compared and rejected. Recorded in 00 Guidelines on the Design system page.

## 24 Sep 2026 · later (Session A)

- EV plan and Places moved out of Profile (P01 back to 8 tiles), Production and Dark.
  - EV plan: link "EV plan · −30 %" on the EV01 card → sheets EV08 (offer) and EV08a (active).
  - Places: one shared half-screen sheet L01, opened from every location row (EV01e Deliver to, EV01d and G01d Where to, TR02 pickup). One saved list for all modules.
  - P10, P11, P11a removed.
- Data sources (Emin): EV is fully real-time. Golf shows what Sea Breeze staff set in the admin panel (no live GPS). Renter and Transfer have no live data; details are agreed in chat.
- Continued Session B's paused queue (it ran out of credits): 2 vision pass, done (G01d2 wording, G02b tray); 4 prototype run, done (flow starts, new links, Profile backdrops); 3 company account screens, waiting for scope.
- Company account screens (Emin chose "with team"): A03c company details, W02b company payment method, W03b invoices, P12 Team sheet. Production and Dark.
- Top spacing under the Dynamic Island (Emin): tab-root titles start at y 100; nav bars, back buttons and camera headers moved from y 59 to y 67; content under them moved 8 pt down. Rule recorded in 00 Guidelines.
- Session B's paused queue is finished. Session A is not editing the file now.
- EV plan is now minute packages: EV08 Monthly, EV08b Weekly, EV08c Yearly, 5 packages each (Production and Dark). Prices are placeholders on the ₼0.25/min base, waiting for Emin.
- Vision pass after the spacing change: HO05, R01g and TR01c backdrops aligned; A06c/A06d hold timer corrected; EV08a label wrap fixed.
- Open: the EV01/EV01d/EV01e tariff control is at 50 % layer opacity (not set by Session A).
- EV tariff row (min / hour / day / Driver) set to full strength on all EV screens, Production and Dark (Emin: easier to read). Handoff row added.
- R01a Dates now shows 28–29 (Production and Dark). EV plan prices stay placeholders; handoff says load them from the backend.
- Consistency check: Production and Dark have the same 113 screens with identical texts. Design system: two sections resized to fit their text, sections re-spaced, 06 SwiftUI guide screen map updated for EV08–EV08c, L01 and company screens.
- New pages "Production flow AZ" and "Production flow RU": exact copies of the 113 Production screens (UI and UX unchanged), prototype links and 23 flow starts re-pointed to the copies, all texts translated. Money shown as "16,00 ₼", thousands with a space. Where a translation did not fit a fixed-size element (tabs, chips, buttons, camera tray), a shorter wording was used. Dictionary: localization/strings-en-az-ru.csv (853 strings). Not yet done: native Russian/Azerbaijani review.
- New page "Developer handoff": one-page index of all screens (by flow, with presentation type), components, tokens, motion and haptics, layout rules, data sources, languages and 10 open questions.
- Component swap: all large buttons were already Button / Large instances (76) and all tab bars are Apple kit instances. The one hand-built button left, "Save card" on W02a, is now a Button / Large instance on all four pages. The Apple Pay button stays native on purpose.
- HO01: one 'Add a car' button replaced by two equal buttons 'Add a car' (→ HO02) and 'Post a transfer' (→ HO07a, then HO07). All four pages; handoff row updated.
- New page "Host & Staff" (after Production flow). Section "07 · Host" moved there from Production flow with its flow starts "07 Host" and "07b Transfer driver". Host sections and their flow starts removed from Production flow AZ and RU. The Hosting tile stays in P01 on all pages; its prototype link cannot cross pages, so it no longer opens HO01. Dark mode page unchanged. Next: in-app staff mode (hidden Admin button in Host, 8-digit staff code, Driver mode, Sea Breeze team mode) on the Host & Staff page.
- Staff and admin inside the app (Emin; brief from the admin panel session): 65 new screens on the "Host & Staff" page, sections 08–14 (ST00–ST61), light and English only. Hidden Admin row in HO01 (hard pull), 8-digit staff code, role homes for full_admin, investor, sea_breeze_team and driver. Page names match the web panel (rentbutik-admin). Prototype links and 5 flow starts ("Staff · …") are set. Contract (roles, statuses, screens): HANDOFF-NOTES.md, and section "12 · Staff and admin" in the Handoff notes frame. Developer handoff page updated (178 screens, open questions 11–15).
- Final split from the admin session (message 4): admin panel = web app in Emin-dev/newiosadmin; staff and drivers stay in the main app. Full admin and Investor screens (sections 11–14) moved to a new page "Admin panel (newiosadmin)" as phone-size drafts. ST01 now routes seabreeze_team → ST20 and drivers → ST10. ST21a now assigns cart, driver and arrival time 5/10/15/20 min. ST09 shows a Sea Breeze team account. Handoff notes frame, Developer handoff page and HANDOFF-NOTES.md updated with the new role codes (admin, seabreeze_team, driver_ev, driver_golf, transfer_host).
- Emin: normal Host flow back on Production flow (y 11340, flow starts "07 Host" and "07b Transfer driver"). AZ and RU Host sections recreated from Production and translated (dictionary + short forms where text did not fit; RU "Разместить трансфер" → "Новый трансфер"), prototype links re-pointed, P01 Hosting tile links to HO01 again on all three pages. "Host & Staff" page now holds only staff and driver versions (sections 08–10). Next: simpler staff UI (one screen per role, 4–6 bento tiles, no scrolling), waiting for Emin's answers.
- Emin: Host on Production is two flows. Flow A · Add a car (HO01 › HO02–HO02d, then HO03 › HO04 › HO04b). Flow B · Post a transfer, now 4 steps like Flow A but with its own fields: HO07a Car check (first time only) › HO07b Route › HO07c When (date, time, repeat, return trip) › HO07d Seats & price › Publish → HO06; then HO08. The old one-screen HO07 was removed; links to it now open HO07b. Two rows with flow labels; sections below moved down 890 pt. Same on AZ and RU (translated).
- Emin: staff UI made simple. Admin now lives in the main app too (same hidden Admin row + phone sign-in). Detailed staff screens and the "Admin panel (newiosadmin)" page removed. "Host & Staff" page: 08 access, 09 Driver (ST10–ST13), 10 Sea Breeze team (ST20–ST26), 11 Admin (ST30–ST36). Every role: one home with 6 bento tiles, no scrolling; decisions (new job, golf request, approvals) take over the screen with big Decline/Accept tiles, one item at a time. Golf requests come with a suggested cart, driver and arrival (10 min). Admin Approvals queue = car listings, documents, transfer car checks, parking appeals. Admin Cars = EVs, golf carts and host cars with on/off. Contract in HANDOFF-NOTES.md.
- Staff screens now also in AZ, RU and Dark: sections "08–11 · … · AZ / · RU / · Dark" on the "Host & Staff" page, to the right of the English ones. AZ/RU translated (money as "16,00 ₼"), long tile subtitles shortened to fit. Dark uses the token Dark mode and the Dark page's tab bar, back button and status bar. Prototype links point inside each copy.
- Staff screens also in AZ Dark and RU Dark (sections "… · AZ Dark", "… · RU Dark", right of the Dark column). RU staff account sheet now ticks Русский. Button labels (Add a car, Post a transfer, Leave staff mode) translated in all AZ/RU copies.
- Emin: staff sign in with their phone number like customers (A07): SMS code or WhatsApp, no 8-digit staff code. ST01 / ST01b / ST01c rebuilt from A07 in all six staff versions (EN, AZ, RU, each light and dark); ST00 and ST09 texts updated.
