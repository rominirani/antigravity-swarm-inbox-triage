# Weekly Customer Inbox Triage Summary (24-Email Batch)

**Date:** November 17, 2026  
**Scope:** `email_01` – `email_24` (24 customer emails, including 2 multi-issue inquiries: `email_11` and `email_19`)

---

## 1. Full 24-Email Mapping (`email_01` – `email_24`)

| Email ID | Customer | Issue Mapping | Status | Summary / Context |
| :--- | :--- | :--- | :--- | :--- |
| `email_01` | Priya Sharma | `NEW UNLISTED BUG` | **UNLISTED (Escalated)** | iPhone app `v4.2` — Apple Pay team plan renewal spins endlessly after Face ID confirms |
| `email_02` | Marcus Bell | `ISS-101` | `FIXED in v4.2` | Blank PDF invoice downloaded from stale browser tab |
| `email_03` | Elena Rostova | `NEW UNLISTED BUG` | **UNLISTED (Escalated)** | iPhone mobile Safari `v4.2` — Apple Pay checkout hangs indefinitely on spinner (card entry works) |
| `email_04` | David Kim | `ISS-102` | `OPEN` | Dark Mode chart axis numbers unreadable (dark gray on black) |
| `email_05` | Nadia Kowalski | `NEW UNLISTED BUG` | **UNLISTED (Escalated)** | macOS Firefox `132` — Google SSO + 2FA redirects back to sign-in screen in an endless loop |
| `email_06` | Sara Al-Mansoor | `ISS-104` | `OPEN` | Team invite email button immediately says "Invite link expired" |
| `email_07` | Omar Hassan | `NEW UNLISTED BUG` | **UNLISTED (Escalated)** | iPhone app `v4.2` — Apple Pay checkout stuck on loading spinner after Face ID sheet closes |
| `email_08` | Claire Bennett | `ISS-103` | `FIXED in v4.1` | MacBook desktop app `v4.0` CSV export stops at 500 rows |
| `email_09` | Kenji Takahashi | `ISS-102` | `OPEN` | Dark Mode dashboard bar chart axis labels unreadable on wall monitor |
| `email_10` | Fatima Zahra | `NEW UNLISTED BUG` | **UNLISTED (Escalated)** | iPhone 16 Pro app `v4.2` — Apple Pay Starter-to-Pro upgrade hangs on infinite spinner after Face ID |
| `email_11` | Lucas Meyer | `ISS-101`, `ISS-104` | `FIXED in v4.2` / `OPEN` | Multi-part: (1) blank PDF invoice download (`ISS-101`); (2) expired workspace invite button (`ISS-104`) |
| `email_12` | Hannah Abbott | `ISS-104` | `OPEN` | Workspace invite email button reports "Invite link expired" within minutes |
| `email_13` | Diego Morales | `NEW UNLISTED BUG` | **UNLISTED (Escalated)** | iPhone mobile Safari `v4.2` — Apple Pay seat expansion spins endlessly after Face ID (manual card works) |
| `email_14` | Mei-Ling Zhou | `ISS-101` | `FIXED in v4.2` | Blank PDF invoices downloaded from pinned Chrome billing tab |
| `email_15` | Ryan O'Neill | `ISS-103` | `FIXED in v4.1` | Analytics CSV export (~2,400 rows) truncates at 500 rows on Windows `v4.0.3` |
| `email_16` | Aisha Patel | `NEW UNLISTED BUG` | **UNLISTED (Escalated)** | iPhone app `v4.2` — Apple Pay annual renewal invoice freezes on loader right after Face ID succeeds |
| `email_17` | Tomas Silva | `ISS-102` | `OPEN` | Dark Mode X/Y axis numbers on dashboard charts nearly unreadable |
| `email_18` | Grace Lindqvist | `ISS-104` | `OPEN` | Team invite email button shows "Invite link expired" within 5 minutes |
| `email_19` | Ben Carter | `ISS-103`, `ISS-102` | `FIXED in v4.1` / `OPEN` | Multi-part: (1) CSV export cuts off at 500 rows on `v4.0` (`ISS-103`); (2) Dark Mode chart axes unreadable (`ISS-102`) |
| `email_20` | Zoe Papadopoulos | `NEW UNLISTED BUG` | **UNLISTED (Escalated)** | iPhone Safari `v4.2` web release — Apple Pay checkout hangs on spinner 10+ min after Face ID |
| `email_21` | Viktor Novak | `ISS-101` | `FIXED in v4.2` | Blank Sept & Oct PDF invoices downloaded from unrefreshed browser window |
| `email_22` | Rachel Goldstein | `NEW UNLISTED BUG` | **UNLISTED (Escalated)** | Firefox `132` — Workspace SSO + mandatory 2FA bounces back to `/login` in an infinite redirect loop |
| `email_23` | Noah Campbell | `NEW UNLISTED BUG` | **UNLISTED (Escalated)** | iPhone / iOS app `v4.2` — Apple Pay storage add-on checkout spins forever after Face ID approves |
| `email_24` | Sofia Rossi | `ISS-104` | `OPEN` | Team invite email button immediately displays "Invite link expired" |

---

## 2. New Unlisted Bugs & Engineering Priorities

Ten of the 24 emails (`41.7%` of inbox volume) report **two new unlisted regressions** absent from `known_issues.csv`:

1. **[P0 — Revenue Blocking] iPhone `v4.2` Apple Pay Infinite Checkout Spinner (8 Customers)**
   - **Affected Emails:** `email_01`, `email_03`, `email_07`, `email_10`, `email_13`, `email_16`, `email_20`, `email_23`
   - **Shared Pattern:**
     - **Device / Environment:** iPhone (affects both the native iOS app and mobile Safari on iOS).
     - **Version:** `v4.2` (iOS app `v4.2` and `v4.2` web release).
     - **Payment Flow:** Apple Pay checkout across upgrades, renewals, extra seats, and storage add-ons. Face ID authenticates and dismisses the Apple Pay sheet, after which the checkout button/page hangs indefinitely on a spinning loader without completing payment or generating a receipt.
     - **Temporary Workaround Observed:** Manual credit/debit card entry completes normally (`email_03`, `email_13`).

2. **[P0 — Auth / Access Blocking] Firefox 132 + SSO + 2FA Infinite Login Redirect Loop (2 Customers / Whole Security Org Affected)**
   - **Affected Emails:** `email_05`, `email_22`
   - **Shared Pattern:**
     - **Browser / Version:** Firefox `132` (confirmed on macOS and enterprise desktops; Chrome and Safari sign in normally).
     - **Login Flow:** Workspace Single Sign-On (`SSO`, including Google SSO) with mandatory Two-Factor Authentication (`2FA`). Immediately after entering a valid 6-digit 2FA code, the session flashes and redirects back to `/login` (sign-in screen) in an endless loop, locking out Firefox 132 SSO+2FA users.
     - **Temporary Workaround Observed:** Signing in via Chrome or Safari bypasses the redirect loop (`email_05`, `email_22`).

---

## 3. Known Issues Volume & Action Summary

- **`ISS-104` (`OPEN` — Team invite email button says link expired): 5 reports** (`email_06`, `email_11`, `email_12`, `email_18`, `email_24`) — Highest-volume known open issue; customers given `Settings > Team > Copy Link` direct URL workaround. Prioritize permanent token/link fix.
- **`ISS-102` (`OPEN` — Dark mode text hard to read on dashboard charts): 4 reports** (`email_04`, `email_09`, `email_17`, `email_19`) — Customers informed fix is scheduled for next week and given `Settings > Appearance > Light Mode` workaround.
- **`ISS-101` (`FIXED in v4.2` — Blank PDF invoice downloads): 4 reports** (`email_02`, `email_11`, `email_14`, `email_21`) — Primarily caused by long-lived/pinned browser tabs running pre-`v4.2` assets; customers instructed to refresh/update to `v4.2`.
- **`ISS-103` (`FIXED in v4.1` — CSV export stops at 500 rows): 3 reports** (`email_08`, `email_15`, `email_19`) — Customers still on `v4.0` / `v4.0.3` desktop builds instructed to update to `v4.1+`.
