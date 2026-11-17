# Customer Inbox Triage Guidelines

Use `inputs/known_issues.csv` and the 6 customer emails in `inputs/emails/` to prepare customer replies and a short weekly summary for the product team.

## Rules for Replying
1. **Check `known_issues.csv` first:**
   - If the customer's problem matches a `FIXED` issue, tell them clearly which version fixed it and share the steps in `customer_guidance`.
   - If the customer's problem matches an `OPEN` issue, be honest that it is still open (never say it is already fixed) and share the workaround in `customer_guidance`.
2. **Spot new unlisted bugs:**
   - If an email describes a problem that is **not** in `known_issues.csv`, apologize, let the customer know you are escalating it to engineering right away, and check whether other emails report the same new problem.

## Required Output Files
Write seven short Markdown files into the target output folder:
1. **`reply_01.md` through `reply_06.md`** — One polite, concise reply email (`5–10` lines) for each corresponding customer (`email_01` through `email_06`), including a clear `Subject:` line.
2. **`weekly_triage_summary.md`** — A 1-page summary for the product and engineering team covering:
   - A quick table mapping all 6 emails (`email_01`–`email_06`) to either a `known_issues.csv` ID (`FIXED` / `OPEN`) or `NEW UNLISTED BUG`.
   - **Top Engineering Priority:** Highlight any new unlisted bug reported by multiple customers, naming which emails reported it and what common pattern they share (device, browser/app version, payment method).
