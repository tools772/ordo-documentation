# Reports

**Reports** is the operations scoreboard. It answers questions like “how many remittances did we post this week?” and “which carrier is stuck in review?” It is **not** a replacement for your accountant’s production reports or Open Dental’s insurance reports.

Open it from the sidebar: **Reports**.

Numbers come from uploaded EOBs your role can see. **Archived files are excluded**, so they cannot inflate the story.

---

## Filters (they stack)

Both controls sit in the page header. Using both together narrows the set.

### Uploaded date

Same control as the EOB Dashboard. Presets include today, last 7 days, last 30 days, and this month. You can also pick a custom range.

The date is **when the file was uploaded to Ordo**, not the date of service on the claim, and not the insurance check date. If Jennifer uploads June’s leftover remittance on August 28, it counts in August.

### EOBs

Pick one or more files. The picker follows the date filter, so you only see EOBs in that range.

**Clear filters** returns to “every active EOB.” A line under the header tells you how many files are in the current set.

Export uses that same filtered set.

---

## Example: Friday wrap-up at Bright Smile

Jennifer wants “this week, Cigna only.”

1. Date preset: **last 7 days**.
2. EOBs: she ticks the three Cigna files from this week, leaves the Delta file unticked.
3. The header says the set contains **3 EOBs**.
4. She glances at pending review and posted payments.
5. She exports for the owner huddle.

If she had left EOB empty, she would have seen Cigna **and** Delta for the week.

---

## Operations overview

The same style of summary as the dashboard — uploads, pending review, posted payments, failed jobs, trends — but computed from **the filtered EOBs**, not the whole inbox.

!!! tip "Today’s uploads inside a filter"
    “Today’s uploads” still means files uploaded today, **and** they must sit inside the current filter. If your date range is last month, today’s uploads will be zero. That is consistent, not a bug.

---

## Processing analytics

You will see counts such as:

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

**Example.** Delta shows 10 uploaded and 2 posted (20% post rate). Cigna shows 10 uploaded and 9 posted. Jennifer does not assume Delta “pays worse.” She opens the two posted Delta files, then the eight unposted ones — often the reader failed on a non-standard layout, or matching needs review. Reports tell her *where to look*. They do not tell her *why* until she opens a file.

---

## What Reports is not

- Not a deposit slip. Posted dollars here are Ordo’s view of EOB plan covered amounts that were posted, not your bank.
- Not a proof of posting for every Open Dental write if someone posted by hand in Open Dental outside Ordo.
- Not including archived files. Archive a duplicate if you do not want it in the scoreboard.

---

## Related pages

- [EOB Dashboard](eob-dashboard.md)
- [A typical Monday morning](../examples/typical-morning.md)
- [When something looks wrong](../examples/when-things-go-wrong.md)
