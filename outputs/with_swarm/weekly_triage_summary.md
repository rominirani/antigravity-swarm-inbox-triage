# Weekly Customer Inbox Triage Summary

**Date:** November 16, 2026  
**Scope:** 6 customer support emails (`email_01`–`email_06`) triaged against `known_issues.csv`

---

## 1. Email-to-Issue Triage Mapping

| Email | Customer | Classification / Issue ID | Status | Summary & Customer Guidance Shared |
| :--- | :--- | :--- | :--- | :--- |
| `email_01` (`email_01_priya.md`) | Priya Sharma | **NEW UNLISTED BUG** | **UNLISTED (Escalated)** | Checkout spins forever after Face ID confirms Apple Pay on iPhone app (`v4.2`). Apologized, escalated to engineering, and suggested manual card entry workaround. |
| `email_02` (`email_02_marcus.md`) | Marcus Bell | `ISS-101` | **FIXED** (`FIXED in v4.2`) | October PDF invoice downloaded as a blank page from an old browser tab. Advised refreshing browser / updating to `v4.2` and downloading again. |
| `email_03` (`email_03_elena.md`) | Elena Rostova | **NEW UNLISTED BUG** | **UNLISTED (Escalated)** | Apple Pay hangs on an infinite spinner on iPhone mobile Safari (`v4.2`), while manual card entry works. Apologized and escalated to engineering. |
| `email_04` (`email_04_david.md`) | David Kim | `ISS-102` | **OPEN** | Dark mode dashboard bar chart axis numbers are hard to read. Confirmed fix is planned for next week; shared temporary workaround (`Settings > Appearance` → Light Mode). |
| `email_05` (`email_05_sara.md`) | Sara Al-Mansoor | `ISS-104` | **OPEN** | Team invite email button immediately reports `"Invite link expired"`. Confirmed issue remains open; shared direct link workaround (`Settings > Team > Copy Link`). |
| `email_06` (`email_06_omar.md`) | Omar Hassan | **NEW UNLISTED BUG** | **UNLISTED (Escalated)** | Checkout freezes on an infinite loading spinner after Apple Pay sheet closes on iPhone (`v4.2`). Apologized and escalated to engineering. |

*(Note: `ISS-103` — CSV export stopping at 500 rows, `FIXED in v4.1` — had zero reports this week.)*

---

## 2. Top Engineering Priority: iPhone `v4.2` Apple Pay Infinite Spinner Regression

A **new unlisted payment-blocking bug** accounted for **3 of 6 tickets (50% of inbox volume)** across both triage batches and directly blocks customer checkouts and plan renewals:

- **Affected Emails:** `email_01` (Priya Sharma), `email_03` (Elena Rostova), and `email_06` (Omar Hassan).
- **Shared Pattern:**
  - **Device / Platform:** **iPhone** — affects both the **native iPhone app** (`email_01`) and **mobile Safari** (`email_03`), with `email_06` also on iPhone.
  - **Version:** **`v4.2`** — all three customers reported the failure immediately after updating to `v4.2` (within the past hour to 24 hours), pointing to a `v4.2` regression.
  - **Payment Flow & Symptom:** Selecting **Apple Pay** at checkout triggers Face ID / the Apple Pay sheet, but once confirmed/closed, the checkout screen hangs indefinitely on a **loading spinner** and never completes the order. Standard manual credit card entry still succeeds (`email_03`).
- **Recommended Action:**
  1. **P0 Engineering Investigation:** Inspect the `v4.2` checkout Apple Pay completion callback / token handoff on iOS (shared web/checkout flow across iPhone app and mobile Safari) and ship a hotfix or rollback.
  2. **Support & Triage Tracking:** Add this regression to `known_issues.csv` as `OPEN` and advise affected iPhone `v4.2` users to pay by entering a card number manually until the fix ships.

---

## 3. Open Known Issues Follow-Up

- **`ISS-102` (`OPEN` — Dark mode chart text contrast, `email_04`):** Keep on track for next week's planned release; Light Mode workaround provided.
- **`ISS-104` (`OPEN` — Team invite email button expired error, `email_05`):** Actively impacting customer onboarding; direct invite URL (`Settings > Team > Copy Link`) unblocks teams in the interim.
