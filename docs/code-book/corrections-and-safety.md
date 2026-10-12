---
search:
  exclude: true
---

# Step 6 — Corrections and safety

**The question:** what can still be changed, by whom, and how do we know who changed it?

The rule of thumb: **anything can be corrected before posting; nothing Ordo posted can be changed in Ordo afterwards.** After posting, Open Dental is the record, and Ordo stays in step with it.

---

## What Ordo does

### 1. What you can edit

With the **Edit extracted data** permission:

| Where | What |
| --- | --- |
| EOB page | Check date and check number |
| Posting list (pencil on each row) | Patient name, subscriber ID, date of birth, claim number, date of service, claim amount, provider |
| A patient's EOB Review | The same patient and claim fields |
| Procedure lines | Code, description, tooth, date, billed, insurance paid, patient share |

### 2. Every edit is written to the audit log

Each saved edit records **who**, **when**, and the **old and new value of only the fields that changed**. Saving without changing anything writes nothing.

### 3. Editing an approved claim clears the approval

Approval freezes the amounts (see [Approving and posting](approving-and-posting.md)). If someone then changes the claim or a procedure line, the frozen plan no longer matches the EOB. So:

- Changing a **claim field** or **procedure line** on an approved claim cancels the approval. The claim goes back to **Needs review**, a message says so, and the cancellation is in the audit log.
- Approving again rebuilds the plan from the edited amounts.
- Editing only the **patient's** name, ID or date of birth does not clear approval, because none of that is sent to Open Dental.

### 4. Posted claims are locked

Once a claim is **Posted** (or **Already Posted** in Open Dental):

- The pencil on that row becomes a lock.
- Edit buttons on the patient's review page are replaced by "Posted to Open Dental — edits are locked so Ordo matches what was posted."
- The server refuses edits too, so the lock cannot be bypassed.

To fix a posted payment, correct it in Open Dental. Ordo's Payment Analysis will flag a difference between the remittance and what is in Open Dental.

### 5. Reprocessing a file

**Reprocess** reads the same PDF again with the latest reader (for example after we fix a layout). It replaces the patients, claims and lines on that EOB and clears fetch results and edits.

- Allowed until **any** claim on the EOB is approved or posted. After that, reprocessing would erase the record that stops Ordo from posting twice, so it is blocked.
- Archived EOBs must be restored first.
- Patients left with no claims after a reprocess are cleaned up.

### 6. Rejecting a match

**Reject match** discards the match and any approval. If you type a remark and the claim is known, Ordo writes "Ordo reject: *your remark*" as a note on the claim's first procedure in Open Dental, so the reason is not lost. Reject is unavailable after posting.

### 7. Privacy and clinic separation

- Patient details are stripped from Ordo's technical logs, including logs of Open Dental searches.
- Open Dental keys never reach the browser.
- Every request is limited to the clinic selected in the header. Ordo never falls back to "the first clinic".

---

## Real cases

!!! example "Edits after posting"
    **What happened.** A clinic asked whether staff could still edit an EOB after its payment was posted to Open Dental. The answer was yes, with no record of who changed what. Ordo and Open Dental could quietly disagree.

    **What Ordo does now.** Posted claims are locked, every edit is audit-logged, and editing an approved claim clears the approval.

!!! example "An edited paid amount that did not stick"
    **What happened.** Ordo stores a line's paid amount in two places. Editing a procedure's insurance-paid amount updated only one of them, while matching, approval and the review screen read the other. The edit looked saved but reverted on refresh and would not have been posted.

    **What Ordo does now.** The edit updates both, so what you type is what gets approved and posted.

!!! example "Fixing a layout after files were already read"
    **What happened.** A reader bug was fixed for a payer, but the clinic's files from that payer had already been read the old way.

    **What Ordo does now.** **Reprocess** re-reads them with the fixed reader, as long as nothing on that EOB has been approved or posted.

---

## What Ordo does not do yet

!!! warning "Known gaps"
    - **Check date and number edits are not kept on reprocess.** Reprocessing reads them from the PDF again.
    - **Undo** — there is no one-click revert of an edit. The audit log shows the old value so you can type it back.
    - **Reject notes** go on the first procedure only.

---

## Questions for your team

!!! question "Have you seen something different?"
    1. Who on your team should be allowed to **edit** extracted data, and who only to **approve** or **post**?
    2. When you find a mistake **after** posting, do you fix it in Open Dental and move on, or do you need Ordo to reflect the correction too?
    3. Do you need to show the audit trail to anyone outside the office (an owner, an auditor, a DSO)?
    4. Are there fields you correct often that Ordo does not let you edit?

---

[← 5. Checking the money](checking-the-money.md) · [The codebook](index.md) · [Next: Edge-case checklist →](edge-case-checklist.md)
