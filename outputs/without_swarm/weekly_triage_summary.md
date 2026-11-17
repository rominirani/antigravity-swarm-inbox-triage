# Weekly Customer Inbox Triage Summary

**Date:** November 17, 2026  
**Total Emails Triaged:** 6 (`email_01` – `email_06`)

## Inbox Mapping Overview

| Email | Customer | Reported Symptom | Triage Classification | Status | Action / Guidance Provided |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `email_01` (`email_01_priya.md`) | Priya Sharma (`priya@brightstudio.co`) | Team plan renewal stuck spinning after Face ID on Apple Pay (iPhone app v4.2) | **NEW UNLISTED BUG** | Escalated (Urgent) | Apologized, escalated to engineering alongside matching reports; shared direct card entry workaround |
| `email_02` (`email_02_marcus.md`) | Marcus Bell (`mbell@northwind.io`) | October PDF invoice downloads as a blank white page from week-old browser tab | `ISS-101` | `FIXED` (in v4.2) | Confirmed fixed in v4.2; asked customer to refresh browser / update to v4.2 and re-download |
| `email_03` (`email_03_elena.md`) | Elena Rostova (`elena@velohealth.org`) | Apple Pay hangs on infinite spinner on iPhone mobile Safari after v4.2 update (card entry works) | **NEW UNLISTED BUG** | Escalated (Urgent) | Apologized, escalated immediately to engineering with confirmation that manual card entry works |
| `email_04` (`email_04_david.md`) | David Kim (`dkim@harborfreight.dev`) | Dark gray chart axis numbers on black background in Dark Mode | `ISS-102` | `OPEN` | Confirmed still open with fix planned for next week; shared workaround (`Settings > Appearance` -> Light Mode) |
| `email_05` (`email_05_sara.md`) | Sara Al-Mansoor (`sara@loomcraft.design`) | Team invite email button immediately says "Invite link expired" | `ISS-104` | `OPEN` | Confirmed still open; shared direct invite URL workaround (`Settings > Team > Copy Link`) |
| `email_06` (`email_06_omar.md`) | Omar Hassan (`omar@fieldstone.co`) | Checkout freezes on loading spinner after Apple Pay sheet closes on iPhone (v4.2) | **NEW UNLISTED BUG** | Escalated (Urgent) | Apologized, confirmed v4.2 Apple Pay bug, escalated to engineering; shared direct card entry workaround |

---

## Top Engineering Priority: New Unlisted Bug (Apple Pay Checkout Hang in v4.2)

**50% of this week's triaged inbox (3 of 6 emails)** reports the same critical, unlisted checkout regression blocking customer payments and plan renewals:

- **Reporting Emails:**
  - `email_01` — Priya Sharma (iPhone native app, updated to v4.2)
  - `email_03` — Elena Rostova (iPhone mobile Safari, updated to v4.2)
  - `email_06` — Omar Hassan (iPhone checkout, updated to v4.2)
- **Shared Pattern Across All Reports:**
  - **Device:** All 3 customers are on **iPhone (iOS)**.
  - **App / Browser Version:** All 3 customers updated to **v4.2** within the past 24 hours. Because it affects both the **iPhone app** (`email_01`) and **mobile Safari** (`email_03`), the regression likely sits in shared v4.2 web/checkout payment handling or backend Apple Pay session completion rather than native-only UI code.
  - **Payment Method & Failure Mode:** Exclusively affects **Apple Pay**. After Face ID authorization / Apple Pay sheet dismissal, checkout hangs indefinitely on a loading spinner and never completes the order. Standard manual credit/debit card entry continues to work (`email_03`).
- **Recommended Immediate Actions:**
  1. Treat as a **P0 revenue-blocking incident** and inspect v4.2 changes to the Apple Pay payment confirmation callback on iOS.
  2. Add a new tracked issue (e.g., `ISS-105`) to `known_issues.csv` with the temporary workaround (pay by entering card details directly) until hotfixed.

---

## Known Issues Pulse

- **Open Issues Driving Support Volume:**
  - **`ISS-102` (`OPEN` — Dark mode chart text readability, 1 report: `email_04`):** Fix remains scheduled for next week; Light Mode workaround communicated.
  - **`ISS-104` (`OPEN` — Team invite email button expired, 1 report: `email_05`):** Actively frictioning customer onboarding; direct link copy workaround communicated.
- **Resolved Issues:**
  - **`ISS-101` (`FIXED in v4.2` — Blank PDF invoice, 1 report: `email_02`):** Triggered only because the user had a stale pre-v4.2 browser tab open from last week.
  - **`ISS-103` (`FIXED in v4.1` — CSV export 500-row limit, 0 reports):** No new customer reports.
