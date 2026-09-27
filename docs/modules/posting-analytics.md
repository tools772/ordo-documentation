# Posting Analytics

**Posting Analytics** is the posting scoreboard. Open it from the sidebar: **Analytics → Posting Analytics**.

It has two tabs:

| Tab | Question it answers |
| --- | --- |
| **Overview** | How many remittances did we upload, post, or fail — and which carrier is stuck? (This is what used to be called **Reports**.) |
| **Missing Posting** | Which claims in Open Dental were sent or received but still have **no insurance payment posted**? |

It is **not** a replacement for your accountant’s production reports or Open Dental’s insurance reports. Nothing here writes to Open Dental.

You need the **View analytics** permission. See [Roles and who can do what](../people/roles.md).

---

## Overview

The Overview starts idle — the card says **Overview is idle**. Click **Load overview** when you want the numbers.

Numbers come from uploaded EOBs your role can see. **Archived files are excluded**, so they cannot inflate the story.

### Filters (they stack)

Both controls sit in the page header. Using both together narrows the set.

**Uploaded date.** Same control as the EOB Dashboard. Presets include today, last 7 days, last 30 days, and this month. You can also pick a custom range.

The date is **when the file was uploaded to Ordo**, not the date of service on the claim, and not the insurance check date. If Jennifer uploads June’s leftover remittance on August 28, it counts in August.

**EOBs.** Pick one or more files. The picker follows the date filter, so you only see EOBs in that range.

**Clear filters** returns to “every active EOB.” A line under the header tells you how many files are in the current set. **Export** uses that same filtered set.

### Operations overview

The same style of summary as the dashboard — uploads, pending review, posted payments, failed jobs, trends — but computed from **the filtered EOBs**, not the whole inbox.

!!! tip "Today’s uploads inside a filter"
    “Today’s uploads” still means files uploaded today, **and** they must sit inside the current filter. If your date range is last month, today’s uploads will be zero. That is consistent, not a bug.

### Processing analytics

| Metric | Plain meaning |
| --- | --- |
| Documents uploaded | How many files are in the set. |
| Payments posted | How many of those files reached posted/completed. |
| Claims posted | Claim-level count (one file can have many claims). |
| Procedure lines | Line-level count. |
| Average processing time | How long reading/processing took, on average. |
| Average review time | How long files sat waiting on a person, when available. |
| Manual corrections | Edits people made to extracted data. |
| Failed syncs | Times talking to Open Dental did not succeed. |

Plus carrier views:

- **Insurance carrier breakdown** — uploaded vs posted counts
- **Payment value by carrier** — posted dollars
- **Carrier performance detail** — per-carrier uploaded, posted, value posted, and post rate

**Example.** Delta shows 10 uploaded and 2 posted (20% post rate). Cigna shows 10 uploaded and 9 posted. Jennifer does not assume Delta “pays worse.” She opens the eight unposted Delta files — often the reader failed on a non-standard layout, or matching needs review. The Overview tells her *where to look*. It does not tell her *why* until she opens a file.

### Example: Friday wrap-up at Bright Smile

Jennifer wants “this week, Cigna only.”

1. **Analytics → Posting Analytics**, tab **Overview**. She clicks **Load overview**.
2. Date preset: **last 7 days**.
3. EOBs: she ticks the three Cigna files from this week and leaves the Delta file unticked.
4. The header says the set contains **3 EOBs**.
5. She glances at pending review and posted payments, then clicks **Export** for the owner huddle.

If she had left EOB empty, she would have seen Cigna **and** Delta for the week.

### What the Overview is not

- Not a deposit slip. Posted dollars here are Ordo’s view of EOB plan covered amounts that were posted, not your bank.
- Not proof of every Open Dental write — someone may have posted by hand in Open Dental outside Ordo. (Missing Posting, below, looks at Open Dental directly.)
- Not including archived files. Archive a duplicate if you do not want it in the scoreboard.

---

## Missing Posting

The page describes itself as: *Claims in Open Dental that are Sent or Received but have no ClaimPayment (EOB) linked.*

In plain words: the claim went out (or the practice marked it received), but no insurance check or EFT has been attached to it in Open Dental. Money may be sitting unposted, or the payer never answered.

This tab looks at **Open Dental**, not at files uploaded to Ordo. It catches claims whether or not their EOB ever came through Ordo.

### Step 1 — Fetch data

On the **1. Fetch data** tab, fill in:

| Field | What to choose |
| --- | --- |
| **Service date** | One date of service. Missing Posting fetches **one day per job**. |
| **Claim status** | **Sent + Received** (default), **Sent only**, or **Received only**. |
| **Claim type** | **All types**, or one type such as Primary. |
| **Edited since** | Only claims changed in Open Dental after this point. Default **Last 90 days**. |

Click **Submit fetch job**. The job appears in the list with a status (see [fetch job statuses](analytics.md#fetch-job-statuses)). You can leave the page while it runs.

### Step 2 — Analyze

On the **2. Analyze** tab:

1. Pick the **Fetch job**.
2. Optional: narrow by **Payer**, or set **Min days outstanding** (for example 30, to see only claims that have waited a month).
3. Click **Run analysis**.

Summary cards: **Claims scanned**, **Missing posting**, **Fee billed**, **Avg days outstanding**.

The table lists each flagged claim: DOS, Patient, Carrier, Status, Days out, Fee billed, Claim, Codes, Remarks, and **How calculated**.

**Days outstanding** counts from the date the claim was sent. If Open Dental has no sent date, Ordo counts from the date of service.

### What the remarks mean

| Remark | What happened | What to do |
| --- | --- | --- |
| **Payment not finalized** | Claim is Received and an insurance amount is typed on the procedures, but it was never attached to a check or EFT — so nothing is actually posted. | In Open Dental, finalize the insurance payment: attach the entered amount to the matching check or EFT. |
| **Received, nothing posted** | Claim is Received but no insurance payment is posted. | Find the EOB or ERA and post it — or post $0 with the denial reason if the payer paid nothing. |
| **No response · 45d** | Claim was sent 30 or more days ago and the payer has not paid or responded. | Call the payer about claim status. If they have no record, resubmit. |
| **Awaiting payer** | Sent less than 30 days ago. Still a normal wait. | Check again later; follow up once it passes 30 days. |

Click **How calculated** on any row for **Why this is missing posting · {patient}**: four short steps (claim status, days outstanding, insurance payment posted, amount waiting on insurance) and a **What to do** box.

### Example: month-end sweep at Bright Smile

Jennifer wants to know what from **March 3** still has no payment.

1. **Missing Posting → 1. Fetch data**. Service date **March 3**, **Sent + Received**, **All types**, **Last 90 days**. **Submit fetch job**.
2. Two minutes later the job is **Complete**. She opens **2. Analyze**, picks the job, sets **Min days outstanding** to 30, and clicks **Run analysis**.
3. Six claims show. Four say **No response · 38d** — she calls those carriers. One says **Payment not finalized** — the check was typed in but never attached, so she finalizes it in Open Dental. One says **Received, nothing posted** — the EOB is in Ordo’s inbox, so she posts it the usual way.

---

## Related pages

- [Analytics](analytics.md) — the four Analytics pages and how fetch jobs work
- [Payment Analytics](payment-analytics.md)
- [EOB Dashboard](eob-dashboard.md)
- [A typical Monday morning](../examples/typical-morning.md)
- [When something looks wrong](../examples/when-things-go-wrong.md)
