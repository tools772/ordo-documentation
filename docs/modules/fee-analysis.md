# Fee Analysis

**Fee Analysis** puts your contracted fees side by side. Open it from the sidebar: **Analytics → Fee Analysis**.

The page describes itself as: *Compare CDT fees across selected insurance schedules and Office / UCR for a specific as-of date.*

Use it to answer questions like:

- “What does Cigna pay for a crown compared with Delta and MetLife?”
- “Which insurer pays furthest below our office fee on cleanings?”
- “Did the fee schedule we uploaded for 2026 actually take effect on January 1?”

It reads the [fee schedules and date maps](../workflows/fee-schedules.md) set up in Clinic settings. Nothing is written anywhere. You need the **View analytics** permission.

---

## Run a comparison

1. **As-of date** — the date you care about. Ordo uses whichever fee schedule each insurer (and Office / UCR) had mapped on that day.
2. **Insurance providers** — tick one or more insurers. Use **Search providers…** on a long list.
3. **CDT codes (optional — comma-separated)** — for example `D0120, D2750`. Leave empty for every code.
4. Click **Run analysis**.

Limits: up to **400** CDT codes and **60** insurers in one run.

---

## Reading the table

The heading says **Fees as of {date}**. Columns: **CDT**, **Description**, **UCR** (your office fee), then one column per insurer you picked. Click a column header to sort. Use **Filter CDT or description…** to narrow the rows.

| You see | Meaning |
| --- | --- |
| A dollar amount | The contracted fee for that code on the as-of date. |
| **—** | No fee for that code in the schedule that applies on that date. |
| A fee in grey | The insurer pays **less than your UCR** for that code. |
| A **parent** badge on an insurer | That insurer has no date map of its own, so Ordo used its parent carrier’s schedule (for example a regional plan using the national Delta schedule). |

Hover an insurer’s column header to see which fee schedule was used and its date range (for example `2026-01-01 → open`). Hover **UCR** to see the Office / UCR schedule — or **No Office / UCR map for this date** if none is mapped.

---

## Example: checking a new schedule took effect

Bright Smile renegotiated with Cigna. Sarah uploaded **Cigna PPO 2026** and mapped it from 2026-01-01.

1. As-of date **2025-12-31**, provider **Cigna**, codes `D1110, D2750`. Cigna shows $96 and $820.
2. As-of date **2026-01-02**, same filters. Cigna shows $104 and $865.

The new schedule is live from January 1. If both runs had shown the old numbers, the date map would be wrong — see [Fee schedules and date maps](../workflows/fee-schedules.md#common-problems).

!!! tip "A column full of —"
    If an insurer shows **—** for almost every code, its schedule for that date is empty or nearly empty. Payment Analytics will then flag those lines as **Fee schedule review** instead of measuring underpayment. Fix the schedule first.

---

## Related pages

- [Fee schedules and date maps](../workflows/fee-schedules.md)
- [Payment Analytics](payment-analytics.md)
- [Analytics](analytics.md)
