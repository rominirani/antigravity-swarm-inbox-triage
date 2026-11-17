# Customer Inbox Triage Guidelines (24-Email Batch)

Use `known_issues.csv` and the 24 customer emails in `emails/` to prepare individual customer replies and a short weekly summary for the product and engineering team.

## Rules for Replying
1. **Check `known_issues.csv` first (including multi-question emails):**
   - If a customer asks about more than one issue in the same email, address **every** question clearly.
   - If an issue matches a `FIXED` item, tell them which version fixed it and share the steps in `customer_guidance`.
   - If an issue matches an `OPEN` item, be upfront that it is still open (never say it is already fixed) and share the workaround in `customer_guidance`.
2. **Spot new unlisted bugs:**
   - If an email describes a problem that is **not** in `known_issues.csv`, apologize, let the customer know you are escalating it to engineering right away, and check whether other emails report the same new problem.

## Required Output Files
Write 25 short Markdown files into the target output folder:
1. **`reply_01.md` through `reply_24.md`** — One polite, concise reply email (`5–12` lines) for each corresponding customer (`email_01` through `email_24`), including a clear `Subject:` line.
2. **`weekly_triage_summary.md`** — A 1-page summary for the product and engineering team covering:
   - A table mapping all 24 emails (`email_01`–`email_24`) to their `known_issues.csv` ID(s) (`FIXED` / `OPEN`) or `NEW UNLISTED BUG`.
   - **New Unlisted Bugs & Engineering Priorities:** List **every** new unlisted bug reported by multiple customers, naming all email IDs that hit each bug and the exact shared pattern (device, browser/app version, login or payment flow).
