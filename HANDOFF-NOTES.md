# Handoff notes · Staff, drivers and admin in the app

Figma: https://www.figma.com/design/Ereat5qYENeSKTvW473gn5/Design-flow
Updated 24 Sep 2026. Emin's decision: staff, drivers and admins all work inside the main app (Emin-dev/iOS), in the Host module, behind the hidden Admin row and an 8-digit code. Every role gets one simple screen: 6 bento tiles, no scrolling. The earlier detailed staff screens and the "Admin panel (newiosadmin)" drafts were removed.

Page "Admin & Staff": sections 08 (access), 09 (Driver), 10 (Sea Breeze team), 11 (Admin). The normal Host flow is on Production flow: Flow A Add a car (HO02–HO02d) and Flow B Post a transfer (HO07a–HO07d).

## Rules for every staff screen
- Drivers and the Sea Breeze team are salaried Rentbutik or Sea Breeze staff: their screens show no money (no fares, earnings, revenue, discounts or deposits). Only admins see money (ST36 Today).
- One home screen per role, 6 tiles (2 × 3), no scrolling. Info tiles show a number; action tiles do one thing.
- Anything that needs a decision takes over the screen: a big card on top, then Decline (red) and Accept (green) tiles. The next item opens right after.
- Lists are short (at most 4–6 items) and fit on the screen.

## How staff get in
1. Profile › Hosting (HO01). A hard pull-down at the top shows a hidden "Admin" row (ST00), like the Telegram archive row.
2. Admin row → ST01, the same sign-in as A07: phone number, Send code, 6-digit code by SMS, or "Get the code on WhatsApp instead". No password, no separate staff code.
3. Only phone numbers linked to a staff account get a code. Wrong or expired code → ST01b (Resend). A number that is not a staff account → ST01c.
4. The backend returns the role and the home: `admin` → ST30, `seabreeze_team` → ST20, `driver_ev` / `driver_golf` / `transfer_host` → ST10. The person button opens ST09 (name, role, phone, language, Leave staff mode).

## 09 · Driver
- ST10 Home (online): Online toggle · Jobs today · Rating · Online today · Messages · Support. ST10b same, offline.
- ST11 New job (takes over the screen): job card (type, route, guests, 0:45 countdown) + Decline / Accept.
- ST12 Active job, arrived: job card + Navigate (Apple Maps) · Call · Message · Cancel job + one big status button "Start ride". ST12b in progress: "End ride".
- One job flow for EV with driver (EV01d), Deliver to me (EV01e), Golf with driver (G01d) and transfers (HO06–HO08). Each driver sees only the job types of their role.

## 10 · Sea Breeze team
- ST20 Home: New requests · On trip · Free carts · Trips today · Messages · Close the day.
- ST21 Request (takes over the screen, one at a time): request card + Suggested cart, driver and arrival time (5 / 10 / 15 / 20 min, 10 pre-selected) + Decline / Accept. "Change" edits the suggestion.
- ST23 On trip: up to 6 cart tiles. ST23a one cart: Extend 1 hour · Change cart · Message · Report damage + big "End trip".
- ST24 Carts: 14 small cart tiles with status; tap turns a free cart off or on.
- ST26 Close the day: 4 totals + big "Close the day".

## 11 · Admin (simple, in the app)
- ST30 Home: Approvals · Messages · Cars · Users · Today · Alerts.
- ST31 Approvals, one at a time: new car listings, documents (MyGov + photos), transfer car checks (HO07a), parking appeals. Decline (asks for a reason) / Approve.
- ST32 Messages: last 4 customer chats → the same chat screen as C03.
- ST33 Cars: search + EV / Golf / Hosts chips + on/off toggle per car.
- ST34 Users: search → one user card + Call · Message · Papers · Block.
- ST35 Alerts: damage, debt, low battery, one button each.
- ST36 Today: totals per module, read-only.
- The full admin panel (statistics, settings, investor view) is not in the app.

## Roles

`GET /admin/me` returns the role. The app shows only what the role allows; the backend blocks the rest. Codes are proposals until the backend confirms them.

| Role code | Who | Home |
|---|---|---|
| `admin` | Rentbutik admins | ST30 |
| `seabreeze_team` | Sea Breeze golf desk | ST20 |
| `driver_ev` | Rentbutik EV drivers | ST10 |
| `driver_golf` | Sea Breeze golf drivers | ST10 |
| `transfer_host` | A host whose HO07a car check is approved | ST10 and HO06–HO08 |

## Status names

| Contract | Values |
|---|---|
| Job (EV with driver, Deliver to me, Golf with driver, Transfer) | `requested`, `accepted`, `driver_on_the_way`, `arrived`, `in_progress`, `completed`, `cancelled` |
| Golf reserve (same as the old web panel) | `pending`, `approved`, `ongoing`, `completed`, `declined_by_admin`, `cancelled_by_user`, `cancelled_by_admin` |
| Golf cart | `available`, `in_use`, `reserved`, `blocked`, `maintenance` |
| P2P trip (same as the old web panel) | `pending`, `accepted`, `ongoing`, `finished`, `declined`, `on_hold`, `cancelled_by_admin`, `cancelled_by_renter`, `cancelled_by_system` |
| Listing review | `in_review`, `needs_changes`, `live` |
| Document check | `waiting`, `verified`, `rejected` |

## Design system

- Tokens, text styles, effect styles and components: Figma page "Design system", collection "Rentbutik · Tokens" (Light and Dark).
- Swift code: `Rentbutik/Design/Theme.swift` in Emin-dev/figma (motion and colour tokens). No shared Swift package exists yet.
- Icons: SF Symbols. The names used are the `Icon / …` components on the Production flow page.

## Changes to existing screens

- The normal Host flow (HO01–HO08) is on Production flow, AZ and RU again. The "Admin & Staff" page holds only the staff and driver versions.
- G01d2: the Sea Breeze team accepts golf requests in the app (ST21a) and picks cart, driver and arrival time.

## Open questions

1. How many wrong codes before the phone is locked out, and for how long: same rule as the customer sign-in (A07).
2. Role codes are proposals. The backend confirms the `/admin/me` shape.
3. Staff screens exist in English, AZ and RU, each in light and dark. A native speaker should review AZ and RU.
4. Daily summary (ST26) needs a backend endpoint.
