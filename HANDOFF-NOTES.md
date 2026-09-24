# Handoff notes · Staff and admin in the iOS app

Figma: https://www.figma.com/design/Ereat5qYENeSKTvW473gn5/Design-flow, page "Host & Staff", sections 08–14 (screens ST00–ST61).
The full tap-by-tap list (motion and haptic for each action) is section "12 · Staff and admin" of the frame "Handoff notes · 24 Sep 2026" on the Production flow page. This file has the same contract in short form for the web admin panel (Emin-dev/newiosadmin) and the iOS team.

Updated 24 Sep 2026.

## How staff get in

1. Profile › Hosting (HO01). A hard pull-down at the top shows a hidden "Admin" row (ST00), like the Telegram archive row. It stays until the user leaves Hosting.
2. Admin row → ST01, a full-screen 8-digit code keypad. The code is checked by the backend on the 8th digit. There is no Continue button.
3. Wrong code → ST01b, "Wrong code. N tries left." After 5 wrong codes → ST01c, locked for 15 min. Both numbers are proposals.
4. On success, Hosting shows the role home. The person button (top right) opens ST09 Staff account: name, role, code ending, language, Leave staff mode.

## Roles

`GET /admin/me` returns the role and permission scopes. The app shows only what the role allows, and the backend blocks everything else. The role codes below are proposals until the backend confirms them.

| Role code | Who | Home | Sees |
|---|---|---|---|
| `full_admin` | Rentbutik team | ST30 | Everything. CEO and Investor switch, all modules, all write actions |
| `investor` | Investors | ST60 | Growth and finance totals only. No personal data, no actions |
| `sea_breeze_team` | Sea Breeze golf desk | ST20 | Golf requests, reserves, trips, fleet, transactions, daily summary. Golf settings read-only |
| `driver` | EV drivers, golf drivers, transfer hosts | ST10 | Online toggle, job inbox, active job, history and earnings |

Write actions (full admin and Sea Breeze team) sit behind the "Actions" switch on the admin home. It is off by default, stays on for 15 min, then turns itself off. Every write also asks for confirmation in a glass alert. This is the same rule as the web panel.

## Status names

| Contract | Values |
|---|---|
| Job (EV with driver, Golf with driver, Transfer) | `requested`, `accepted`, `driver_on_the_way`, `arrived`, `in_progress`, `completed`, `cancelled` |
| Golf reserve (same as the web panel) | `pending`, `approved`, `ongoing`, `completed`, `declined_by_admin`, `cancelled_by_user`, `cancelled_by_admin` |
| Golf cart | `available`, `in_use`, `reserved`, `blocked`, `maintenance` |
| P2P trip (same as the web panel) | `pending`, `accepted`, `ongoing`, `finished`, `declined`, `on_hold`, `cancelled_by_admin`, `cancelled_by_renter`, `cancelled_by_system` |
| Listing review | `in_review`, `needs_changes`, `live` |
| Document check | `waiting`, `verified`, `rejected` |

## Screens

Page names match the web panel so both clients read the same backend.

### 08 · Staff access
ST00 Hosting, Admin revealed · ST01 Staff code · ST01b Wrong code · ST01c Locked · ST09 Staff account (sheet)

### 09 · Driver
ST10 Jobs (Online on) · ST10b Offline · ST11 Job offer (sheet, 0:45 to accept) · ST12 Active job (map, rider, status steps, one button per step) · ST12a Cancel job (alert) · ST13 History and earnings

### 10 · Sea Breeze team (Golf desk)
ST20 Golf desk · ST21 Requests · ST21a Approve and assign cart (sheet) · ST22 Reserves · ST23 On trip · ST23a End trip (alert) · ST23b Discount (sheet) · ST24 Fleet (carts, models, block and unblock) · ST25 Transactions · ST26 Daily summary (new, not in the web panel)

### 11 · Full admin · EV
ST30 Admin home (CEO view, EV) · ST31 Users · ST31a User detail · ST31b Block user (alert) · ST32 Vehicles · ST32a Vehicle detail · ST33 Trips · ST33a Trip detail · ST34 Map · ST35 Reserves · ST36 Outstanding debt · ST37 Damage reports · ST38 Statistics · ST39 EV settings

### 12 · Full admin · P2P
ST40 P2P home · ST41 Users · ST42 Vehicles · ST42a Vehicle detail · ST43 Trips · ST43a Trip detail · ST43b Cancel trip (alert) · ST44 Reviews · ST45 Ops queues · ST46 Notifications · ST47 Marketplace settings

### 13 · Full admin · Golf settings, Transfer and platform
ST27 Golf settings · ST50 Transfer home (car checks, 10 % fee) · ST51 Transfers · ST52 Listing review · ST52a Ask for changes (sheet) · ST53 Document checks · ST53a Document check detail (MyGov + 5 photos) · ST54 Company accounts · ST54a Company detail (VÖEN, team limit, invoices) · ST55 EV plans · ST56 Support inbox · ST57 Parking warnings and appeals · ST58 News and notifications · ST58a New message (sheet) · ST59 Staff and roles · ST59a Add staff member (sheet, creates the 8-digit code)

### 14 · Investor
ST60 Investor overview (investor login) · ST60b Admin in Investor view · ST61 Investor · Golf

## Changes to existing screens

- The Host flow (HO01–HO08) moved from Production flow to the "Host & Staff" page. It was removed from the AZ and RU pages. The Hosting tile stays in P01, but the prototype link from P01 no longer crosses pages.
- G01d2: Sea Breeze staff now accept golf requests in the app (ST21a) or in the web panel.

## Open questions

1. Lockout values (5 tries, 15 min) are proposals.
2. Role codes are proposals. The backend confirms the `/admin/me` shape.
3. Host & Staff screens are light and English only. AZ, RU and Dark copies are not made yet.
4. Driver earnings (ST13) and Daily summary (ST26) need backend endpoints.
