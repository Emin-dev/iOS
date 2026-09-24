# Handoff notes · Staff, drivers and admin panel

Figma: https://www.figma.com/design/Ereat5qYENeSKTvW473gn5/Design-flow
Updated 24 Sep 2026, after the final split of work from the admin panel session.

- The main app (Emin-dev/iOS) is for Sea Breeze team members and drivers, in the Host module. Page "Host & Staff", sections 08–10, screens ST00–ST26.
- The admin panel (Emin-dev/newiosadmin) is for Rentbutik admins. Draft frames are on page "Admin panel (newiosadmin)", sections 11–14, screens ST27 and ST30–ST61. They are phone size for now; the web layout is an open question.

The tap-by-tap list with motion and haptic for each action is in section "12 · Staff and drivers in Host" of the frame "Handoff notes · 24 Sep 2026" on the Production flow page.

## Staff and drivers in the main app

### How they get in
1. Profile › Hosting (HO01). A hard pull-down at the top shows a hidden "Admin" row (ST00), like the Telegram archive row. It stays until the user leaves Hosting.
2. Admin row → ST01, a full-screen 8-digit code keypad. The backend checks the code on the 8th digit. There is no Continue button.
3. Wrong code → ST01b, "Wrong code. N tries left." After 5 wrong codes → ST01c, locked for 15 min. Both numbers are proposals.
4. On success, Hosting shows the role home: `seabreeze_team` → ST20, `driver_ev` / `driver_golf` / `transfer_host` → ST10. The person button opens ST09 Staff account (role, code ending, language, Leave staff mode).

### Screens
- 08 · Staff access: ST00 Hosting, Admin revealed · ST01 Staff code · ST01b Wrong code · ST01c Locked · ST09 Staff account (sheet)
- 09 · Driver: ST10 Jobs (Online on) · ST10b Offline · ST11 Job offer (sheet, 0:45 to accept) · ST12 Active job (map, rider, status steps, one button per step) · ST12a Cancel job (alert) · ST13 History and earnings. One inbox for EV with driver (EV01d), Deliver to me (EV01e), Golf with driver (G01d) and transfers (HO06–HO08). Each driver sees only the job types of their role.
- 10 · Sea Breeze team: ST20 Golf desk · ST21 Requests · ST21a Assign cart, driver and arrival time (5 / 10 / 15 / 20 min) · ST22 Reserves · ST23 On trip · ST23a End trip (alert) · ST23b Discount (sheet) · ST24 Fleet (block and unblock carts and models) · ST25 Transactions · ST26 Daily summary

Still missing from the brief: extend a golf rental and return photos on the Sea Breeze side. The guest side has them (G03a, G02b).

## Roles

`GET /admin/me` returns the role and permission scopes. The app shows only what the role allows, and the backend blocks everything else. These codes are proposals until the backend confirms them.

| Role code | Who | Where |
|---|---|---|
| `admin` | Rentbutik admins. CEO view and Investor view with a switch | Admin panel only |
| `seabreeze_team` | Sea Breeze golf desk | Main app, ST20 |
| `driver_ev` | Rentbutik EV drivers | Main app, ST10 |
| `driver_golf` | Sea Breeze golf drivers | Main app, ST10 |
| `transfer_host` | A host whose HO07a car check is approved | Main app, ST10 and HO06–HO08 |

## Status names

| Contract | Values |
|---|---|
| Job (EV with driver, Deliver to me, Golf with driver, Transfer) | `requested`, `accepted`, `driver_on_the_way`, `arrived`, `in_progress`, `completed`, `cancelled` |
| Golf reserve (same as the old web panel) | `pending`, `approved`, `ongoing`, `completed`, `declined_by_admin`, `cancelled_by_user`, `cancelled_by_admin` |
| Golf cart | `available`, `in_use`, `reserved`, `blocked`, `maintenance` |
| P2P trip (same as the old web panel) | `pending`, `accepted`, `ongoing`, `finished`, `declined`, `on_hold`, `cancelled_by_admin`, `cancelled_by_renter`, `cancelled_by_system` |
| Listing review | `in_review`, `needs_changes`, `live` |
| Document check | `waiting`, `verified`, `rejected` |

## Admin panel frames (page "Admin panel (newiosadmin)")

- 11 · Admin · EV: ST30 Admin home (CEO view, module chips, Actions switch) · ST31 Users · ST31a User detail · ST31b Block user · ST32 Vehicles · ST32a Vehicle detail · ST33 Trips · ST33a Trip detail · ST34 Map · ST35 Reserves · ST36 Outstanding debt · ST37 Damage reports · ST38 Statistics · ST39 EV settings
- 12 · Admin · P2P: ST40 P2P home · ST41 Users · ST42 Vehicles · ST42a Vehicle detail · ST43 Trips · ST43a Trip detail · ST43b Cancel trip · ST44 Reviews · ST45 Ops queues · ST46 Notifications · ST47 Marketplace settings
- 13 · Admin · Golf settings, Transfer and platform: ST27 Golf settings · ST50 Transfer home (car checks, 10 % fee) · ST51 Transfers · ST52 Listing review · ST52a Ask for changes · ST53 Document checks · ST53a Document check detail · ST54 Company accounts · ST54a Company detail · ST55 EV plans · ST56 Support inbox · ST57 Parking warnings and appeals · ST58 News · ST58a New message · ST59 Staff and roles · ST59a Add staff member (creates the 8-digit code)
- 14 · Admin · Investor: ST60 Investor overview · ST60b Admin in Investor view · ST61 Investor · Golf

Not drafted yet from the brief's list: Promo codes, Security groups, Car data, Localization, Filters, Golf tariffs and zones as separate pages. They appear only as rows in the settings screens.

Write actions follow the old panel's rule: an "Actions" switch that is off by default, turns itself off after 15 min, and a confirm alert for every write.

## Design system for the admin panel

- Tokens, text styles, effect styles and components: Figma page "Design system", collection "Rentbutik · Tokens" (Light and Dark).
- Swift code: `Rentbutik/Design/Theme.swift` in Emin-dev/figma (motion and colour tokens). No shared Swift package exists yet.
- Icons: SF Symbols. The names used are the `Icon / …` components on the Production flow page.

## Changes to existing screens

- The normal Host flow (HO01–HO08) is on Production flow, AZ and RU again. The "Host & Staff" page holds only the staff and driver versions.
- G01d2: the Sea Breeze team accepts golf requests in the app (ST21a) and picks cart, driver and arrival time.

## Open questions

1. Lockout values (5 tries, 15 min) are proposals.
2. Role codes are proposals. The backend confirms the `/admin/me` shape.
3. Host & Staff screens are light and English only. AZ, RU and Dark copies are not made yet.
4. Driver earnings (ST13) and Daily summary (ST26) need backend endpoints.
5. Admin panel layout: web (desktop) or phone. The drafts are phone size.
