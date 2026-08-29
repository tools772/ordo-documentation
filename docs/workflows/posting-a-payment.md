# Post a payment

This is the full ritual, from a PDF on the desk to money sitting on the Open Dental claim. Read it once end to end. Then keep it as a checklist.

**Nothing is written to Open Dental until Post payment.** Approve is only a confirmation.

---

## Who does which step

At a small office one person may do everything (Owner or Admin). At Bright Smile they split the work on purpose:

| Step | Bright Smile | Role that is allowed to |
| --- | --- | --- |
| Upload the PDF | Jennifer | Upload EOBs |
| Fetch and review | Mike | View EOBs; edit if needed |
| Approve match | Mike | Approve match |
| Post payment | Jennifer | Post payment |
| Spot-check Reports | Sarah | View reports |

A Reviewer **cannot** post. That is a safety rail, not an insult. If your office wants reviewers to post, an Owner can clone a role and tick **Post payment**.

---

## Before you start

- You are in the right **mode**. Demo is practice. Actual is live. See [Demo vs Actual](demo-vs-actual.md).
- In Actual, Open Dental is **connected** and has been **synced** recently ([Clinic settings](../modules/clinic-settings.md)).
- You have the remittance PDF (Cigna Dental standard layout is what Ordo reads today).

---

## Step 1 — Put the file in the inbox

1. Open **EOB Dashboard**.
2. Click **Upload EOBs**.
3. Drop `Cigna_Remit_Aug24.pdf`.
4. Wait until the row says **Extracted** (not Extracting, not Failed).

If it fails, stop and see [When something looks wrong](../examples/when-things-go-wrong.md). Do not post from a failed file.

---

## Step 2 — Open the file and fetch

1. Click the row.
2. Tick the patients you will work (start with one if you are learning: **Maria Santos**).
3. Click **Fetch Open Dental**.
4. Wait for fetch to finish.

!!! warning "Do not skip Fetch"
    Opening Maria before fetch only shows the EOB. The Open Dental tab will look empty. Fetch first, every time.

---

## Step 3 — Read the EOB side

1. Click **Maria Santos**.
2. Stay on **EOB Review**.
3. Confirm name, subscriber, date of service, and procedure amounts against the PDF if anything looks odd.

**Our example numbers:**

- Date of service: June 12
- D0150 comprehensive exam — plan covered **$42.00**
- D1110 prophylaxis — plan covered **$100.00**
- Total to post: **$142.00**

If a name is garbled, fix it here (if you can edit) *before* you trust the match.

---

## Step 4 — Pick the Open Dental claim

1. Open the **Open Dental** tab.
2. Look at the candidate list. The recommended row is pre-selected when Ordo is confident.
3. Confirm it is the June 12 visit, not last year’s cleaning.

If the recommended claim is wrong, click the right candidate. If none are right, **Reject match** and handle that payment in Open Dental by hand (or wait for a better sync).

If you see **Hard mismatch**, do **not** approve. Open **Audit**. Pick another claim or reject.

---

## Step 5 — Read the procedure lines

Check each line:

| EOB code | EOB amount | Open Dental | What you want |
| --- | --- | --- | --- |
| D0150 | $42.00 | Same code, same dollars to write | Status **Match** |
| D1110 | $100.00 | Same code, same dollars to write | Status **Match** |

Remarks start as **Match** or **Not matched**. You may edit them (for example `Cigna paid $100 cleaning — patient copay separate`). After a successful post, remarks become read-only. **Post payment** stays available.

The optional **Add remark to Open Dental** box at the bottom is a *payment-level* note, not a line note.

More detail: [Matching and remarks](matching-and-remarks.md).

---

## Step 6 — Approve match

Click **Approve match**.

You should see a confirmation that the EOB claim is tied to the Open Dental claim number, and that **nothing was posted yet**.

Maria’s row should move to **Approved**.

If the button is missing, your role does not include Approve. Ask an Admin.

If the button is disabled, you likely have a hard mismatch or no candidate selected.

---

## Step 7 — Post payment

Someone with **Post payment** clicks **Post payment**.

In **Demo**, this is a simulation. In **Actual**, Ordo writes `InsPayAmt` on the matched Open Dental procedures (unless those lines are already on a check with the same amount) and sends the notes.

A **popup** reports the result. On success you should see **ClaimPaymentNum** when Open Dental returns one. On failure, use **View audit** for the Open Dental calls. Keep that payment number if the dentist asks “did it really post?”

Maria’s row should say **Posted**. **Post payment** stays available so you can confirm. **Reject match** does not.

If posting fails, do not click it ten times. Approve again only after you have looked at the chart. Open [When something looks wrong](../examples/when-things-go-wrong.md), [Open Dental errors](../errors/open-dental.md), and the patient’s **Audit** tab.

---

## Step 8 — Optional wrap-up

- Repeat for the next patient on the same file.
- Check **Reports** with this week’s date filter: posted count should have moved.
- If the whole file was a duplicate test, **Archive** it so it does not clutter Reports.

---

## Pocket checklist

- [ ] Correct mode (Demo vs Actual)
- [ ] File extracted, not failed
- [ ] Fetch Open Dental
- [ ] Right patient, right date of service
- [ ] No hard mismatch
- [ ] Line amounts look like the PDF
- [ ] Approve
- [ ] Post (right person)
- [ ] Confirmation / payment number

---

## Related pages

- [What each operation does](operations.md)
- [Statuses](statuses.md)
- [Open Dental errors](../errors/open-dental.md)
- [Inside an EOB](../modules/working-an-eob.md)
- [Matching and remarks](matching-and-remarks.md)
- [A typical Monday morning](../examples/typical-morning.md)
