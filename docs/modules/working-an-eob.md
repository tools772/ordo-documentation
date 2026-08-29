# Inside an EOB

This is the screen you get after you click a file on the [EOB Dashboard](eob-dashboard.md). One remittance, all of its patients, and the place you actually approve and post.

The page has two layers:

1. **The patient list** for this file (the “who is on this check?” table).
2. **One patient at a time**, with three tabs: **EOB Review**, **Open Dental**, and **Audit**.

---

## The patient list

Each row is a person Ordo read from the PDF. You will typically see name, patient / subscriber identifiers, claim, date of service, procedure count, amount, Open Dental id (after a match), and a **review status**.

### Search, sort, pages

- Search by name, identifiers, subscriber, or claim-ish text.
- Click a column header to sort.
- Change page size (5, 10, 25, 50) if the remittance is long.

### Checkboxes and Fetch Open Dental

This is the most important habit on the page.

1. Tick one or more patients you are about to work.
2. Click **Fetch Open Dental**.
3. Wait until the fetch finishes.
4. Then open a patient.

Fetch loads matching chart data from Ordo’s copy of Open Dental. **Opening a patient before fetch only shows the EOB side.** People often think the Open Dental tab is “broken” when they skipped this step.

**Example.** Mike ticks Maria Santos and James Lee, clicks **Fetch Open Dental**, then opens Maria. The Open Dental tab now lists claim candidates. If he had opened Maria first, he would have stared at an empty or EOB-only panel and wasted five minutes.

You can fetch again later if someone just posted a claim in Open Dental and you need a fresh copy.

---

### Review statuses on the row

| Status you might see | What to do |
| --- | --- |
| **Not fetched** | Tick the patient, click **Fetch Open Dental**, then open the row. |
| **Pending** | Matching has not decided yet. Fetch if you have not; then look. |
| **Needs review** | Ordo is unsure, or identity checks failed. Open **Audit**. |
| **Approved** | Someone confirmed the claim. Ready to post (if your role allows). |
| **Posted** | Payment is in Open Dental. You are done with this person on this file. **Post payment** stays available to confirm. |
| **Rejected** | Match was thrown away. Decide whether to try another claim or leave it. |
| **No match** | No plausible Open Dental claim. Search the chart; you may need to post by hand in Open Dental. |
| **Failed** | Fetch or a later step failed. Retry fetch; check API logs if it keeps failing. |

The file can stay **Extracted** while people on it are in different statuses. Full map: [Statuses](../workflows/statuses.md).

---

## Tab 1 — EOB Review

This is “what the insurance company wrote,” as Ordo read it.

You will see the extracted patient, their claims, and procedure lines: CDT codes, dates, plan covered amounts.

If your role includes **Edit extracted data**, you can correct a misspelled name or a wrong amount *before* matching. Fix the EOB side here when the PDF was read slightly wrong. Do not “fix” Open Dental by editing this tab — Open Dental is the next tab.

**Example.** The PDF printed `MARIA SANTOS` but Ordo captured `MARIA SANT0S` (zero instead of O). Mike edits the last name on EOB Review, fetches again, and the match confidence jumps.

---

## Tab 2 — Open Dental

This is the posting desk. Full walkthrough: [Matching and remarks](../workflows/matching-and-remarks.md).

In short:

1. Ordo lists **claim candidates**. The recommended one is pre-selected when it is confident.
2. You compare procedure lines:

    | Column | Meaning |
    | --- | --- |
    | **EOB** | Plan covered amount from the remittance. |
    | **Open Dental** | What Ordo will write as `InsPayAmt`, plus the Open Dental procedure number when matched. |
    | **Difference** | Leftover when the EOB line has no matching Open Dental procedure. |
    | **Status** | Match or Differs. |
    | **Remark** | Editable note on that line. |

3. You **Approve match** (still nothing written).
4. You **Post payment** (writes amounts and notes). A popup reports success or the error.
5. Or you **Reject match** if it is the wrong visit.

!!! danger "Hard mismatch"
    If the candidate shows **Hard mismatch**, identity checks failed (patient, date of service, or procedure codes). Amounts might still add up. **Do not approve** until you pick a different claim or reject. Open **Audit** to see which check failed.

If Open Dental changed after you approved, Ordo will ask you to review again rather than overwrite quietly.

After a successful post you should see a **popup**, including the Open Dental claim payment number when the API returns one. **Post payment** stays available. Which buttons work at each status: [Statuses](../workflows/statuses.md).

---

## Tab 3 — Audit

Two things live here:

1. **Open Dental audit** — every fetch, reject remark, and post for this EOB. Copy the report when a write fails.
2. **Match audit** — the “show your work” list. Each **signal** is one comparison:

- Patient ID
- Patient name
- Date of service
- Payer
- Provider
- Procedure codes
- Amount reconciliation

A failed signal reads in plain language, for example:

> Patient name mismatch — EOB has MARIA SANTOS. Open Dental has MARIA SANTOS-LEE.

Use Audit when:

- Status is **Needs review**
- You see **Hard mismatch**
- A post failed (use **View audit** on the popup, or open this tab)
- The dollars match but your gut says it is the wrong visit (twins, same last name, two cleanings in one month)

---

## Other buttons on this page

- **Export** — download this file’s current view (or the open patient tab).
- Summary / board panels — totals for the remittance, useful on a long file.
- Back to dashboard — returns to the inbox. Your work is saved; you do not “lose” an approval by leaving.

---

## Worked example (one patient)

**File:** `Cigna_Remit_Aug24.pdf`  
**Patient:** Maria Santos  
**EOB:** D0150 (exam) plan covered $42.00; D1110 (cleaning) plan covered $100.00  
**Open Dental:** Claim 18421, same date of service, same two codes.

1. Mike selects Maria, clicks **Fetch Open Dental**.
2. He opens Maria. EOB Review shows $142.00 total plan covered.
3. Open Dental tab recommends claim **18421**. Both lines say **Match**.
4. Audit: all signals green.
5. Mike clicks **Approve match**. Toast: nothing posted yet.
6. Jennifer (who can post) clicks **Post payment**.
7. A popup appears with a claim payment number. Maria’s row says **Posted**. **Post payment** stays available.

If step 3 had recommended last year’s claim instead, Mike would pick the June 12 claim from the candidate list — or **Reject match** and stop.

---

## Related pages

- [Post a payment](../workflows/posting-a-payment.md) — the full ritual
- [What each operation does](../workflows/operations.md)
- [Statuses](../workflows/statuses.md)
- [Matching and remarks](../workflows/matching-and-remarks.md)
- [When something looks wrong](../examples/when-things-go-wrong.md)
- [Open Dental errors](../errors/open-dental.md)
