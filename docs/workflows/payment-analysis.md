# Payment Analysis inside an EOB

Every EOB and every patient on it has a **Payment Analysis** tab. It checks one thing: **did the insurance company pay the contracted fee on this remittance?**

It sits next to the posting work, but it is separate from it:

- **Posting** (Approve match, Post payment) is about getting the money into Open Dental.
- **Payment Analysis** is about whether that money was the *right amount*.

Payment Analysis never writes to Open Dental and never changes what you post.

---

## Where to find it

| Level | Tabs | What Payment Analysis shows |
| --- | --- | --- |
| **Whole EOB** (the patient list) | **Posting** · **Payment Analysis** | Every patient on the remittance, totaled. |
| **One patient** | **EOB Review** · **Payment Analysis** · **Open Dental** · **Audit** | That patient’s procedure lines, one by one. |

---

## The rule

The same rule is used everywhere in Ordo. Per procedure:

| Step (as labelled in the formula) | Plain meaning |
| --- | --- |
| **Patient’s share** | Deductible plus coinsurance from the EOB. If those are missing, Ordo uses the EOB’s patient responsibility. |
| **Clinic ↔ insurance contract** | The **contracted** fee for this CDT code, from the insurer’s fee schedule mapped on the date of service. |
| **What insurance paid** | The paid amount. |
| **Underpayment** | Expected minus Paid, never below zero — where Expected is Contracted minus the patient’s share, also never below zero. |

Lines are calculated one at a time, then added up for the patient and the EOB.

The formula footer says it plainly: *Billed (UCR) and EOB Allowed are shown elsewhere for context — they are not used in this underpayment number.*

**Example.** Maria Santos, D2750 crown. Cigna contract: $865. Patient’s share: $432.50 (50% coinsurance). Expected: $432.50. Cigna paid $380. Underpayment: **$52.50**.

---

## Whole-EOB Payment Analysis

Open a file, then click the **Payment Analysis** tab above the patient list.

1. Click **Run analysis** (or **Run again** to refresh). The time shows as **Analyzed at …**.
2. Read the cards: **Status**, **Underpayment**, **Flagged procedures**, **Open work items**.
3. Scan the table: Patient, Lines, Contracted, Patient portion, Expected, Paid, Underpay, Status, Remarks.
4. Click **How calculated** for the math on a patient, or **Open** to jump to that patient’s Payment Analysis.

Tick **Show EOB context (not used in underpayment)** to see Billed and EOB Allowed alongside — handy when talking to the payer, but they do not change the number.

**Results are saved.** Next time anyone opens the tab, the last run loads with the fee schedule, UCR schedule, and time it used. Run again after you fix a fee schedule or edit the extracted lines.

---

## One patient’s Payment Analysis

Open a patient and click **Payment Analysis**. It loads the saved result, or runs automatically if there is none. Click **Refresh** to recalculate.

Each procedure line has a status:

| Status | Plain meaning |
| --- | --- |
| **On contract** | Paid what the contract says. Nothing to do. |
| **Valid adjustment** | Paid less, but for a normal reason. |
| **Fee schedule review** | Ordo could not find a contracted fee, so it cannot judge. |
| **Internal posting** | The gap looks like how the payment was recorded, not the payer. |
| **Potential underpayment** | Paid below the contract. Worth a look. |

---

## When you see NA

**NA** means “Ordo cannot give an honest number here,” not “zero.”

| What shows NA | Why | What to do |
| --- | --- | --- |
| **Contracted**, **Expected**, **Underpay** — status **Fee schedule review**, remark **Missing clinic fee** | No contracted fee was found for this insurer, code, and date of service. | Add or fix the insurer’s fee schedule or date map, then run again. See [Fee schedules and date maps](fee-schedules.md). |
| **Patient portion**, **Expected**, **Underpay** — remark **Patient share unclear** | The EOB’s deductible + coinsurance and its patient responsibility disagree by more than 50 cents, so Ordo cannot tell which is right. | Read the EOB line yourself. If a real gap remains, decide it in **Review** (below). |

Ordo does not treat it as unclear when the patient responsibility is simply billed minus paid — that is a common layout, and Ordo handles it.

---

## Remarks you might see

| Remark | Plain meaning |
| --- | --- |
| **Missing clinic fee** | No contracted fee for this code on this date. |
| **Patient share unclear** | The EOB’s patient amounts disagree (see NA above). |
| **Insurance paid more than contract** | Paid above the contract. Usually fine — but check the fee schedule is current. |
| **Contract fee doesn't match EOB** | The EOB’s allowed amount differs from your contracted fee. Your schedule may be out of date, or the payer used the wrong one. |
| **Paid more than EOB allowed** | Paid is higher than the EOB’s allowed amount — often a reading or layout issue worth a glance. |

---

## Work items and priority

A flagged procedure becomes a **work item** when the gap is at least **$10** or **5%** of expected. Work items also show up in [Payment Analytics → Remittances](../modules/payment-analytics.md#remittances), so an office manager can sweep them across many EOBs.

| Priority | When |
| --- | --- |
| **Critical** | Insurance was expected to pay something and paid **$0**. |
| **High** | Gap of $25 or more, or 10% or more. |
| **Staff action** | Gap of $10 or more, or 5% or more. |

---

## Deciding a line (Review)

On a patient’s Payment Analysis, click **Review** on a flagged line. The **Underpayment review** dialog asks for a decision:

| Decision | Use it when |
| --- | --- |
| **Confirm Underpayment** | The payer really paid short. You plan to appeal or call. |
| **Valid Adjustment** | There is a normal reason (downgrade, alternate benefit, frequency limit). |
| **Fee Schedule Incorrect** | Our fee schedule is wrong, not the payer. Fix the schedule. |
| **Not an Underpayment** | Ordo flagged it, but it is fine. |
| **Needs Manual Review** | Someone else should look (for example the owner or billing company). |

A **reason is required**. The decision closes or updates the work item, so it drops out of the **Needs review** list in Payment Analytics.

Anyone who can open the EOB can run and read Payment Analysis. Recording a decision needs the **Edit extracted data** permission (Owners, Admins, and Reviewers by default).

---

## Example: Monday at Bright Smile

1. Jennifer posts Maria Santos’s Cigna payment as usual.
2. She clicks the EOB-level **Payment Analysis** tab and **Run analysis**. Status shows one flagged procedure: Maria’s crown, **Potential underpayment**, $52.50, priority **High**.
3. She clicks **How calculated**. Contract $865, patient’s share $432.50, paid $380.
4. She opens Maria → **Payment Analysis** → **Review**, picks **Confirm Underpayment**, and types “Appeal sent to Cigna 3/9 — contract rate $865.”
5. James Lee on the same EOB shows **NA** with **Missing clinic fee** on D0431. Cigna’s 2026 schedule has no D0431 line. Sarah adds it under Clinic settings, and Jennifer clicks **Run again**.

---

## Related pages

- [Inside an EOB](../modules/working-an-eob.md)
- [Payment Analytics](../modules/payment-analytics.md)
- [Fee schedules and date maps](fee-schedules.md)
- [Fee Analysis](../modules/fee-analysis.md)
