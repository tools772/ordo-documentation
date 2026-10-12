---
search:
  exclude: true
---

# Steps 3 and 4 — Approving and posting to Open Dental

**The question:** what exactly will be written to Open Dental, and when should Ordo refuse?

Approving and posting are separate on purpose. **Approve** freezes the plan. **Post** carries it out. At Bright Smile, Mike approves and Jennifer posts, but one person can do both if your roles allow it.

---

## Step 3 — Approve: freeze the plan

When Mike clicks **Approve match**, Ordo:

1. **Re-reads** the EOB claim and the Open Dental copy and scores the chosen claim again. If the claim is no longer a valid match for this patient, or now has a hard mismatch, approval is refused.
2. **Writes down the plan** (the "snapshot"), and stops recalculating:
    - which Open Dental claim and which procedure gets which **insurance-paid** amount,
    - the **check number** (from the remittance),
    - the **check date**,
    - the **check amount** and carrier name,
    - each line's note.
3. Marks the other candidates as not chosen.

From here on, posting uses the snapshot, not the EOB as it is now. That is why editing an approved claim clears the approval — see [Corrections and safety](corrections-and-safety.md).

### Which date becomes the check date

Open Dental needs a real date. Ordo uses the first one that exists:

1. The **payment date** printed on the remittance.
2. The claim's **processed date**.
3. **Today.**

The claim's *received* date is never used — that is when the payer received the claim, not when they paid it. If the payment date is missing, the EOB page warns you and lets you type it before you post.

---

## Step 4 — Post: what Ordo writes, in order

When Jennifer clicks **Post payment**, Ordo first runs three checks. Any of them stops the post before anything is written:

| Check | If it fails |
| --- | --- |
| Has Ordo **already posted** these exact procedures? | Marked **Posted** again. Nothing is written twice. |
| Is Open Dental **connected**, and does the snapshot have a claim number? | Stops with an error. |
| Has the Open Dental claim **changed since approval**? (a procedure removed, a code changed, or a line already holding a different paid amount) | **Needs review.** Re-fetch and approve again. |

Then, in this order:

1. **Each matched procedure.** Insurance paid is set to the planned amount, status to **Received**, and the line's note is written.
    - Already on a check **with the same amount** → only the note is updated. That line counts as posted.
    - Already on a check **with a different amount** → Ordo stops: **Needs review**, "already posted with $X; Ordo planned $Y".
2. **Procedures on the claim but not on the remittance.**
    - If they hold $0 and are not on a check → set to **Received at $0**, note "Not on remittance — Ordo". Open Dental will not mark a claim received while any line is still "not received".
    - If they already hold money → Ordo stops and asks you to sort the line out in Open Dental first.
3. **The claim** → status **Received**, date received = check date.
4. **The check** (Open Dental "claim payment") → created with the check number, check date, amount, carrier and your optional payment remark. If part of the claim is already on a check, that check is reused instead of creating a second one.
5. **Verify.** Ordo reads the procedures back from Open Dental and confirms each one holds the planned amount (within 1 cent). If not → **Needs review**.

Only after verification does the claim show **Posted**, and Ordo records exactly which procedures it posted so it can never post them twice.

### Never written to Open Dental

- Write-offs and adjustments
- Deductible applied
- Patient portion
- "Paid by other insurance"

---

## Real cases

!!! example "Payment already entered by hand"
    **What happened.** Jennifer had already posted a check by hand in Open Dental. Ordo tried to post it again and Open Dental refused: "cannot change InsPayAmt when status is received and attached to a claim payment". Testers saw it as an Ordo failure.

    **What Ordo does now.** If the line is already on a check with the **same** amount, that is success: **Already Posted**, and nothing is written. If the amount is **different**, the claim goes to **Needs review** with both amounts shown, and nothing is overwritten.

!!! example "A zero-paid EOB with no payment date"
    **What happened.** An EOB where every line was denied had no payment date. Ordo sent a blank check date and Open Dental rejected the post.

    **What Ordo does now.** The check date falls back to the processed date, then today. Printed dates like `09/24/2026` and `Sep 24, 2026` are both understood. The EOB page warns when the payment date is missing and lets you set it.

!!! example "A bundled procedure that was never on the remittance"
    **What happened.** Open Dental's claim had a `D9910` (desensitizing) the payer bundled and never listed. Open Dental would not mark the claim received because that line was still "not received", so the post failed.

    **What Ordo does now.** Leftover $0 lines are set to Received at $0 with the note "Not on remittance — Ordo". If a leftover line already has money on it, Ordo stops instead of guessing.

!!! tip "Safeguard — the claim changed after approval"
    **The situation.** Mike approves in the morning. At lunch someone removes a procedure from the claim in Open Dental. The afternoon post would write to a procedure that no longer exists.

    **What Ordo does.** Just before writing, Ordo compares the snapshot with the live claim. A removed procedure, a changed code, or a line that already holds a different amount sends the claim to **Needs review**.

!!! tip "Safeguard — a slow connection while creating the check"
    **The situation.** Ordo automatically retries Open Dental requests that time out. For the request that **creates the check**, a retry could create a second check if the first one actually went through.

    **What Ordo does.** Creating a check is never retried automatically. If it fails, the claim goes to review and a person decides.

---

## What Ordo does not do yet

!!! warning "Known gaps"
    - **Write-offs, adjustments and deductibles are not posted.** Ordo posts insurance paid only. Contractual write-offs still need to be entered in Open Dental.
    - **One check per claim, not one per remittance.** A remittance paying five claims becomes five claim payments in Open Dental, each with the remittance's check number. Your deposit total is the sum of the five.
    - **The check amount includes unmatched lines.** If an EOB line had no matching Open Dental procedure, its dollars are still in the check amount but are not posted to any procedure.
    - **The line note replaces the existing note** on each Open Dental procedure. The default note is "Match".
    - **Supplemental payments** on a claim that is already received are not posted as a supplemental; they end in Needs review.

---

## Questions for your team

!!! question "Have you seen something different?"
    1. After posting insurance paid, what do you do next in Open Dental — **write-offs**, adjustments, patient balance transfers? Would you want Ordo to do any of that?
    2. Do you need **one** claim payment per remittance check (one deposit line), or is one per claim fine for your bank reconciliation?
    3. Do you rely on the **procedure notes** in Open Dental for anything? Is overwriting them with "Match" a problem?
    4. How do you handle a **supplemental** or **corrected** payment on a claim you already received?
    5. Which date do you use as the **check date** — the date printed on the check, the EFT date, or the day it hit the bank?
    6. When a payer takes back money (**recoupment** or negative line), how do you post it today?

---

[← 2. Finding the patient and claim](finding-the-patient-and-claim.md) · [The codebook](index.md) · [Next: 5. Checking the money →](checking-the-money.md)
