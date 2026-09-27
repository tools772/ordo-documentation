# Payment Analytics

**Payment Analytics** answers one question: **did the insurance company pay what our contract says they should?** Open it from the sidebar: **Analytics → Payment Analytics**.

It has two tabs:

| Tab | Looks at | Use it for |
| --- | --- | --- |
| **Remittances** | EOBs uploaded to Ordo | This week’s underpayments, across many EOBs at once. |
| **Historical Analysis** | Past claims in Open Dental | Looking back over months of claims, including ones that never came through Ordo. |

Both compare what was paid against the **contracted fee** in your clinic’s [fee schedules](../workflows/fee-schedules.md). If a payer has no fee schedule mapped for the date of service, Ordo cannot say whether they underpaid — the line is flagged for fee schedule review instead.

Nothing here writes to Open Dental. You need the **View analytics** permission.

---

## How underpayment is worked out

The same rule is used everywhere in Ordo (Remittances, Historical Analysis, and [Payment Analysis inside an EOB](../workflows/payment-analysis.md)). Per procedure:

1. **Contracted** — the fee your clinic agreed with this insurer for this CDT code, on this date of service.
2. **Expected** — Contracted minus the **patient’s share** (deductible and coinsurance). Never below zero.
3. **Paid** — what insurance actually paid.
4. **Underpayment** — Expected minus Paid. Never below zero.

Line underpayments are added up for the claim, patient, or EOB.

!!! note "UCR and EOB Allowed are for context only"
    Your office fee (UCR / billed) and the EOB’s **Allowed** amount are shown next to the numbers so you can compare, but they are **not** used to calculate the underpayment. Only the contracted fee is.

**Example.** Maria Santos, D1110 cleaning. Cigna contract says $100. Her coinsurance is $20, so Expected is $80. Cigna paid $65. Underpayment: **$15**.

---

## Remittances

Use this tab to sweep many uploaded EOBs at once, instead of opening each one.

### Filters

| Filter | Meaning |
| --- | --- |
| **Payer** | One insurer, or **All payers**. |
| **EOB** | One file, or **All EOBs (in scope)**. |
| **Payment / upload date** | Date range for the EOBs. |
| **Work item status** | Defaults to **Needs review**. Other choices: All statuses, Confirmed, Valid adjustment, Fee schedule incorrect, Not underpayment, Manual review, Closed. |

The line under the filters says how many extracted EOBs are in scope.

### Load or run

The page starts with **Results stay idle**.

- **Load saved results** — show work items from earlier runs. Fast.
- **Run analysis (N)** — analyze the N EOBs in scope now. The button counts up (**Analyzing 3/12…**) as it goes.

### What you see

Cards: **EOBs in scope**, **Open work items**, **Potential underpayment**, **Expected vs paid**.

The **Underpayment work items** table lists one row per flagged procedure: EOB, Payer, DOS, CDT, Priority, Contracted, Expected, Paid, Underpay, and **Open**.

A procedure becomes a **work item** when the gap is at least **$10** or **5%** of expected. Priority:

| Priority | When |
| --- | --- |
| **Critical** | Insurance was expected to pay something and paid **$0**. |
| **High** | Gap of $25 or more, or 10% or more. |
| **Staff action** | Gap of $10 or more, or 5% or more. |

Click **Open** to jump into that EOB’s **Payment Analysis** tab, where you decide the line (confirm the underpayment, mark it a valid adjustment, and so on). See [Payment Analysis inside an EOB](../workflows/payment-analysis.md#deciding-a-line-review).

**Example.** Monday, Jennifer sets Payer to **MetLife**, date to **last 30 days**, and clicks **Run analysis (7)**. Eleven work items appear; two are Critical ($0 paid on a crown and an exam). She opens the crown first.

---

## Historical Analysis

Use this tab to look back over past claims straight from Open Dental — for example, “has Delta been underpaying fillings all year?”

It works in two steps: **1. Fetch data**, then **2. Analyze**. The general idea is on [Analytics → Fetch first, then analyze](analytics.md#fetch-first-then-analyze).

### Step 1 — Fetch data

The **Data Fetch Jobs** panel:

1. Pick a **Service date** range — up to **30 days** per job. (Historical pulls **Received** claims.)
2. Optional **Description**, so you recognize the job later (“Delta Q1 fillings”).
3. Click **Fetch Data from Open Dental**.

Click **Load recent jobs** to see the job list. Each job shows its status (Queued, Fetching, Complete, Partially complete, Failed) and buttons:

| Button | What it does |
| --- | --- |
| **Analyze** | Jump to step 2 with this job selected. |
| **See claims** | Open the job page: **Overall** progress, **Run history**, and the **Fetched claims** list. |
| **Archive** | Hide the job from the list. An archived job is never reused. |

On the job page, **Retry errored dates** re-fetches only the days that failed. **Retry**, **Re-fetch**, and **Dismiss** handle a failed or stale job.

Need more than 30 days? Submit one job per month. Ordo will not duplicate a job that is already running.

### Step 2 — Analyze

1. Pick the **Fetch job**.
2. Optional: narrow to one **Payer**.
3. Click **Run analysis**.

Switch views to slice the result: **Lines**, **By insurance**, **By CDT**, **By status**, **By month**. Toggle **Show flagged only** / **Show all lines**.

The **Lines** view columns: Patient, Payer, Claim, DOS, CDT, Status, Remarks, Contracted, Expected, OD paid, Underpay, and **How calculated**.

### Line status

| Status | Plain meaning |
| --- | --- |
| **NO UNDERPAYMENT** | Paid as expected. |
| **POTENTIAL UNDERPAYMENT** | Paid below the contracted amount. |
| **POTENTIAL UNDERPAYMENT REQUIRES REVIEW** | Looks short, but something needs a person to check first. |
| **FEE SCHEDULE REVIEW** | No contracted fee was found for this payer, code, and date. Fix the fee schedule, then re-run. |
| **INTERNAL POSTING REVIEW** | The problem looks like how the payment was posted in Open Dental, not the payer. |
| **VALID ADJUSTMENT** | A gap that has a normal explanation. |
| **CONTRACT FEE MISMATCH** | Paid amount does not line up with the contract in a way that needs a look. |

### What the remarks mean

| Remark | What to do |
| --- | --- |
| **No contract fee** | Link or update the fee schedule for this payer in Clinic settings, then re-run analysis. |
| **Frequency limit** | Paid $0 and the payer cited a frequency limit. Not an underpayment — only appeal if the patient’s history shows the remark is wrong. |
| **Paid $0 · payer remark** | Read the payer remark and the EOB before treating this as an underpayment. |
| **Likely not covered** | Paid $0 and Open Dental also estimated $0 — usually not covered (age or frequency). Confirm on the EOB before chasing it. |
| **Paid $0 · check EOB** | Could be a denial, or the payment may have been posted to another line in Open Dental. |
| **Paid below contract** | Insurance paid less than the contract. Compare with the EOB allowed amount, then appeal if the contract applies. |
| **On contract** | No action needed. |

Click **How calculated** for **Why this underpayment · {patient}**: the step-by-step math plus **Open Dental details** — Billed (UCR), OD estimate, OD paid, Deductible, Write-off, and which Fee schedule was used.

### Example: Delta fillings, first quarter

1. Sarah submits three fetch jobs: January, February, March (each under 30 days).
2. When all three are **Complete**, she analyzes January with Payer **Delta Dental**.
3. **By CDT** shows D2392 (two-surface filling) flagged on 14 lines, all **Paid below contract** by about $12.
4. She opens **How calculated** on one line: the fee schedule used is **Delta PPO 2026**, contracted $148, OD paid $136.
5. She repeats for February and March, then sends Delta one appeal with the pattern.

---

## Related pages

- [Payment Analysis inside an EOB](../workflows/payment-analysis.md)
- [Fee schedules and date maps](../workflows/fee-schedules.md)
- [Fee Analysis](fee-analysis.md)
- [Analytics](analytics.md)
- [Posting Analytics](posting-analytics.md)
