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
