---
search:
  exclude: true
---

# Step 5 — Checking the money

**The question:** did the payer pay what your contract says they should?

This is **Payment Analysis** on an EOB, and the **Payment Analytics** module across many EOBs. It reads; it never writes to Open Dental. How to use the screens is in [Check for underpayments on an EOB](../workflows/payment-analysis.md). This page is the arithmetic behind them.

---

## What Ordo does

### 1. The one formula

For each procedure line:

> **Underpaid = contracted fee − patient share − insurance paid**

- **Contracted fee** comes from the clinic's fee schedule for that payer, using the schedule **in effect on the date of service**. See [Set up fee schedules and date maps](../workflows/fee-schedules.md).
- **Patient share** is what the remittance says the patient owes (deductible + coinsurance).
- **Insurance paid** is what the remittance says the payer paid.

Two numbers Ordo deliberately does **not** use as the contracted fee:

- **Your office fee (UCR).** Billed minus paid is shown separately as "vs UCR" for context. It is never called an underpayment.
- **The payer's printed allowed amount.** Shown as "vs Allowed" only when the remittance prints one.

### 2. When Ordo will not guess

A line goes to **review** — with no underpayment dollars — instead of being scored when:

| Situation | Review type |
| --- | --- |
| No fee schedule for this payer on that date | Fee-schedule review |
| Patient share is ambiguous (printed amounts contradict each other) | Review |
| The line is part of a **dual insurance** claim | COB review (see below) |
| The payer's remark mentions coordination of benefits or a secondary payer | COB review |
| The remark mentions a downgrade or alternate benefit | Downgrade review |
| The remark mentions a frequency limit, benefit maximum or annual max | Frequency / maximum review |
| The remark mentions bundling or "inclusive" | Bundling review |

Ordo never adjusts dollars for these. It only recognises the wording and hands the line to a person.

### 3. How serious is it?

- **$0 paid** when money was expected is **critical**.
- A payer remark like "FQ: Last serviced on…" is labelled **Frequency limit** and shown as information, not an underpayment.
- $0 paid when Open Dental also estimated $0 is explained as expected.
- If the amount posted in Open Dental differs from the remittance by more than **$0.50**, the line is flagged for an **internal posting correction** — the payer did nothing wrong, the posting did.
- A claim that already has an open follow-up does not get a second work item.

### 4. Dual insurance

When the primary and secondary insurers each pay part of a procedure:

- Ordo pairs the primary and secondary lines for the same procedure.
- The **primary** line is scored on what **both** insurers paid together.
- A shortfall is flagged **once**, on the primary line only.
- **Secondary** lines go to COB review with no underpayment dollars, even when there is no fee schedule.
- Open Dental's "-1" amount (meaning "not known") is treated as unknown, not as minus one dollar.

### 5. Claims missing a posting

For claims that should have been paid but show nothing posted, Ordo explains which of these it is:

- Received, with a payment entered but not finalized.
- Received, with nothing posted.
- Sent more than **30 days** ago with no response.
- Recently sent — still waiting on the payer.

---

## Real cases

!!! example "Dual insurance flagged as underpaid"
    **What happened.** Maria has two dental plans. Her primary paid $64 on a crown prep and her secondary paid $36. Ordo scored the secondary line on its own and flagged a large underpayment that did not exist. The clinic reported it as feedback.

    **What Ordo does now.** The two payments are added together and scored once, on the primary line. The secondary line is sent to COB review with no dollars attached.

!!! example "MetLife's patient amount"
    **What happened.** For MetLife, the stored patient amount was billed − paid, which includes the write-off. Using it as the patient share made underpayments look smaller than they were.

    **What Ordo does now.** The coinsurance printed on the remittance wins over a calculated billed − paid figure.

!!! example "A frequency denial is not an underpayment"
    **What happened.** A second cleaning inside the plan's frequency window came back $0 with the remark "FQ: Last serviced on…".

    **What Ordo does now.** That remark is labelled **Frequency limit** and shown as information, so nobody chases the payer for it.

!!! tip "Safeguard — underpaid is not the same as billed minus paid"
    **The situation.** Comparing what the payer paid to your office fee makes nearly every in-network line look underpaid.

    **What Ordo does.** Only the contracted fee from your fee schedule is used. Billed − paid is shown as "vs UCR" and never counted as an underpayment.

---

## What Ordo does not do yet

!!! warning "Known gaps"
    - **No fee schedule, no score.** Lines for a payer without a schedule (or with a schedule that does not cover the date of service) go to review. Fee schedules are only as good as what the clinic loads.
    - **Plan rules are not evaluated.** Downgrades, frequency limits, maximums and bundling are only recognised from the payer's remark wording. If the remark uses different words, the line is scored as a possible underpayment.
    - **Waiting periods, missing-tooth clauses, age limits and exclusions** are not recognised at all yet. Lines denied for these reasons show as possible underpayments.

---

## Questions for your team

!!! question "Have you seen something different?"
    1. When a payer pays **less than the contract**, which reasons are legitimate in your experience (annual maximum, alternate benefit, waiting period)? How do you tell them apart on the remittance?
    2. Do you appeal underpayments under a certain dollar amount, or is there a threshold where it is not worth it?
    3. Do you load **every** payer's fee schedule, or only the big ones? Which payers are missing?
    4. For dual insurance, does your secondary usually pay up to the **primary's allowed** or up to **your fee**?
    5. Are there payers whose remittance remarks you would like translated into plain language?

---

[← 3–4. Approving and posting](approving-and-posting.md) · [The codebook](index.md) · [Next: 6. Corrections and safety →](corrections-and-safety.md)
