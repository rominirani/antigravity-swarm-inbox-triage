# Weekly Customer Inbox Triage Summary (Nov 17, 2026)

**Overview:** Triaged **24 customer emails** (`email_01`–`email_24`, representing 26 total issue reports due to two 2-part emails: `email_11` and `email_19`). **14 emails** matched existing entries in `known_issues.csv`, while **10 emails** surfaced **2 critical new unlisted multi-customer regressions** requiring immediate engineering escalation.

## Email-to-Issue Mapping (`email_01`–`email_24`)

| Email ID | Customer | Issue Mapping & Status | Context & Guidance Provided |
| :--- | :--- | :--- | :--- |
| `email_01` | Priya Sharma (`brightstudio.co`) | `NEW UNLISTED BUG` (Apple Pay v4.2 spinner) | iPhone app v4.2 team renewal hangs post-Face ID; escalated + shared manual card/desktop workaround |
| `email_02` | Marcus Bell (`northwind.io`) | `ISS-101` (`FIXED` in v4.2) | Blank Oct PDF from old browser tab; advised browser refresh / v4.2 update & re-download |
| `email_03` | Elena Rostova (`velohealth.org`) | `NEW UNLISTED BUG` (Apple Pay v4.2 spinner) | iPhone mobile Safari v4.2 hangs on Apple Pay (manual card works); escalated repro to engineering |
| `email_04` | David Kim (`harborfreight.dev`) | `ISS-102` (`OPEN`) | Unreadable Dark Mode chart axes; shared next-week fix ETA + `Settings > Appearance` Light Mode workaround |
| `email_05` | Nadia Kowalski (`cobaltlabs.io`) | `NEW UNLISTED BUG` (Firefox 132 SSO+2FA loop) | macOS Firefox 132 + Google SSO + 2FA loops back to login (Chrome works); escalated immediately |
| `email_06` | Sara Al-Mansoor (`loomcraft.design`) | `ISS-104` (`OPEN`) | Invite email button says expired; confirmed still open + shared `Settings > Team > Copy Link` workaround |
| `email_07` | Omar Hassan (`fieldstone.co`) | `NEW UNLISTED BUG` (Apple Pay v4.2 spinner) | iPhone v4.2 checkout freezes on spinner after Face ID; escalated + shared manual card/desktop workaround |
| `email_08` | Claire Bennett (`summitops.com`) | `ISS-103` (`FIXED` in v4.1) | MacBook v4.0 CSV cuts off at 500 rows; advised updating to v4.1+ for automatic full exports |
| `email_09` | Kenji Takahashi (`kestrelmedia.jp`) | `ISS-102` (`OPEN`) | Wall-monitor Dark Mode chart contrast; confirmed still open (fix next week) + Light Mode workaround |
| `email_10` | Fatima Zahra (`crescentpay.co`) | `NEW UNLISTED BUG` (Apple Pay v4.2 spinner) | iPhone 16 Pro v4.2 Pro upgrade hangs after Face ID; escalated + shared manual card/desktop workaround |
| `email_11` | Lucas Meyer (`alpineworks.de`) | `ISS-101` (`FIXED` in v4.2) + `ISS-104` (`OPEN`) | Addressed both: (1) refresh tab/v4.2 for blank PDF; (2) `Settings > Team > Copy Link` for open invite bug |
| `email_12` | Hannah Abbott (`cloverfield.org`) | `ISS-104` (`OPEN`) | Copywriter invite button expired; confirmed still open + shared `Settings > Team > Copy Link` workaround |
| `email_13` | Diego Morales (`solarisenergy.mx`) | `NEW UNLISTED BUG` (Apple Pay v4.2 spinner) | iOS Safari v4.2 seat purchase spins post-Face ID (manual Visa worked); escalated repro details |
| `email_14` | Mei-Ling Zhou (`harborview.hk`) | `ISS-101` (`FIXED` in v4.2) | Blank Oct PDF from pinned Chrome tab; advised refreshing tab / updating to v4.2 and re-downloading |
| `email_15` | Ryan O'Neill (`oakridgefreight.com`) | `ISS-103` (`FIXED` in v4.1) | Windows v4.0.3 CSV stops at 500 rows; confirmed fixed in v4.1 and advised updating app |
| `email_16` | Aisha Patel (`vervebio.com`) | `NEW UNLISTED BUG` (Apple Pay v4.2 spinner) | iPhone app v4.2 annual renewal freezes post-Face ID; escalated + shared manual card/desktop workaround |
| `email_17` | Tomas Silva (`luzstudio.pt`) | `ISS-102` (`OPEN`) | Dark Mode X/Y axis contrast; confirmed open (fix planned next week) + Light Mode workaround |
| `email_18` | Grace Lindqvist (`nordiccraft.se`) | `ISS-104` (`OPEN`) | 3 interns hit expired invite button; confirmed open + shared `Settings > Team > Copy Link` workaround |
| `email_19` | Ben Carter (`redwoodmetrics.io`) | `ISS-103` (`FIXED` in v4.1) + `ISS-102` (`OPEN`) | Addressed both: (1) update from v4.0 to v4.1+ for full CSV; (2) Dark Mode open (next week), use Light Mode |
| `email_20` | Zoe Papadopoulos (`aegeantech.gr`) | `NEW UNLISTED BUG` (Apple Pay v4.2 spinner) | iOS Safari v4.2 web checkout hangs 10+ min post-Face ID; escalated + shared manual card workaround |
| `email_21` | Viktor Novak (`danubedata.cz`) | `ISS-101` (`FIXED` in v4.2) | Blank Sept/Oct PDFs from old open window; advised refreshing browser / v4.2 update & re-downloading |
| `email_22` | Rachel Goldstein (`meridiansec.com`) | `NEW UNLISTED BUG` (Firefox 132 SSO+2FA loop) | Security/eng org on Firefox 132 + SSO + 2FA stuck in `/login` loop (Chrome/Safari work); escalated urgently |
| `email_23` | Noah Campbell (`clearwater.ca`) | `NEW UNLISTED BUG` (Apple Pay v4.2 spinner) | iOS app v4.2 storage add-on hangs post-Face ID; escalated + shared manual card workaround |
| `email_24` | Sofia Rossi (`altavista.it`) | `ISS-104` (`OPEN`) | New PM invite button expired; confirmed still open + shared `Settings > Team > Copy Link` workaround |

## New Unlisted Bugs & Engineering Priorities

### 1. [P0 — Checkout & Revenue Regression] iOS v4.2 Apple Pay Infinite Spinner After Face ID (`8 emails`)
- **Affected Emails:** `email_01`, `email_03`, `email_07`, `email_10`, `email_13`, `email_16`, `email_20`, `email_23`
- **Exact Shared Pattern:**
  - **Device & Platform:** iPhone / iOS, reproducing in **both** the **native iOS app** (`email_01`, `email_07`, `email_10`, `email_16`, `email_23`) and **iOS mobile Safari** (`email_03`, `email_13`, `email_20`).
  - **App / Web Version:** Newly introduced in **v4.2** (every report occurred immediately after updating to the v4.2 app or v4.2 web release).
  - **Payment Flow:** All checkout flows using **Apple Pay** (team/annual renewals, Starter-to-Pro upgrades, extra seat purchases, storage add-ons). Face ID authentication succeeds and the Apple Pay sheet dismisses, but the checkout screen stays stuck on an infinite loading spinner without completing the charge or issuing a receipt. Manual credit/debit card entry on the same v4.2 checkout screen succeeds (`email_03`, `email_13`).
- **Action Needed:** Inspect v4.2 Apple Pay payment-authorization completion handler across iOS app and mobile Safari WebKit; ship emergency hotfix and track in `known_issues.csv`.

### 2. [P0/P1 — Enterprise Auth Lockout] Firefox 132 + SSO + 2FA Infinite Login Redirect Loop (`2 emails`, org-wide impact)
- **Affected Emails:** `email_05`, `email_22`
- **Exact Shared Pattern:**
  - **Device & Browser Version:** Desktop **Firefox 132** (confirmed on macOS in `email_05` and across an entire Firefox 132-standardized security/engineering organization in `email_22`). Chrome and Safari sign in normally (`email_05`, `email_22`).
  - **Login Flow:** Signing in via **SSO** (Google SSO in `email_05`, corporate SSO in `email_22`) with mandatory **two-factor authentication (2FA)**. Immediately after entering the 6-digit 2FA code, the app flashes and redirects straight back to `/login` in an endless loop.
- **Action Needed:** Audit SSO + 2FA post-verification session cookie/redirect handling under Firefox 132 cookie/storage policies; prioritize hotfix to unblock enterprise SSO+2FA teams and add to `known_issues.csv`.

## Known Issues Volume Snapshot
- **`ISS-104` (`OPEN` — Team invite email button says link expired):** 5 reports (`email_06`, `email_11`, `email_12`, `email_18`, `email_24`) — highest-volume open known bug; prioritize email invite token fix alongside unlisted P0s.
- **`ISS-102` (`OPEN` — Dark mode dashboard chart contrast):** 4 reports (`email_04`, `email_09`, `email_17`, `email_19`) — keep on track for next week's release.
- **`ISS-101` (`FIXED in v4.2` — Blank PDF invoice):** 4 reports (`email_02`, `email_11`, `email_14`, `email_21`) — residual hits from stale pre-v4.2 browser tabs.
- **`ISS-103` (`FIXED in v4.1` — CSV export stops at 500 rows):** 3 reports (`email_08`, `email_15`, `email_19`) — residual hits from v4.0/v4.0.3 desktop installs.
