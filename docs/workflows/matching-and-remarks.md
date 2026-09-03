# Matching and remarks

Matching is two jobs:

1. **Which Open Dental patient is this?** — [Finding the patient](finding-the-patient.md)
2. **Which Open Dental claim is this EOB talking about, and which procedure line is which?** — this page

Names on the remittance and names in the chart often disagree. Use **Find possible patients** on the Open Dental tab so you do not have to edit the EOB name just to locate the chart. Then **Fetch Open Dental** and score claims as below.

You do claim matching on the **Open Dental** tab after **Fetch Open Dental**. See [Inside an EOB](../modules/working-an-eob.md) for the screen layout.

---

## How Ordo picks a claim (in human terms)

Ordo looks at the extracted patient and scores Open Dental patients and claims using things like:

- First and last name (small spelling differences are tolerated)
- Date of birth
- Subscriber ID
- Date of service
- Procedure codes (CDT)
- Amounts

A high-confidence match is pre-selected. A middling or “two charts look alike” result is marked for **Needs review**. A very low score is **No match**.

You are always allowed to pick a different **candidate** from the list. Ordo’s recommendation is a starting point, not a court order.

---

## Identity vs money

Two different questions:

1. **Is this the right person and the right visit?** (identity)
2. **Do the dollars add up?** (reconciliation)

A hard mismatch means identity failed. **Do not approve** just because the dollars happen to match. Wrong patient + right dollar amount is still the wrong post.

Open the **Audit** tab. Each **signal** is one check:

| Signal | Example of a failure |
| --- | --- |
| Patient ID | EOB member ID does not match the chart. |
| Patient name | EOB has MARIA SANTOS. Open Dental has MARIA SANTOS-LEE. |
| Date of service | EOB June 12 vs chart July 3. |
| Payer / provider | Unexpected carrier or rendering provider. |
| Procedure codes | EOB has D1110; chart claim has D0120 only. |
| Amount reconciliation | Line totals do not line up. |

Failed signals are written in plain language so you can read them to a coworker without decoding scores.

---

## Procedure lines

Once a claim candidate is selected, each EOB line is compared to Open Dental procedures.

| Column | Meaning |
| --- | --- |
| **EOB** | Plan covered amount from the remittance. This is what Ordo intends to post. |
| **Open Dental** | The `InsPayAmt` that will be written, and the Open Dental procedure number when a line is matched. |
| **Difference** | Leftover when the EOB line has no matching Open Dental procedure. |
| **Status** | **Match** or **Differs** (computed). |
| **Remark** | Your note on that line. |

Default remarks:

- **Match** — the CDT code mapped to an Open Dental claim procedure.
- **Not matched** — it did not.

You can edit the remark until a successful post. After post, remarks are read-only.

### Example — extra EOB line

Cigna paid a D1110 cleaning **and** a D0274 bitewings. Open Dental’s claim only has the cleaning (bitewings were entered on a different claim).

- D1110 row: **Match**, $100.00
- D0274 row: **Not matched**, difference showing, no Open Dental procedure number

Mike does **not** approve this candidate if the bitewings belong on another claim. He switches candidate — or rejects and posts the bitewings on the correct claim later. Approving here would post the cleaning and leave the bitewings unexplained.

### Example — same codes, different dollars

EOB D1110 plan covered $100. Open Dental estimated $80. That can still be a **Match** on code with a dollar difference. Read Audit amount reconciliation. If this is the right visit, posting $100 is often exactly what you want (the EOB is the source for what insurance paid). If it is the wrong visit, reject.

---

## The two kinds of remarks

| Kind | Where you type it | Where it lands in Open Dental |
| --- | --- | --- |
| **Procedure remark** | The Remark column on each line | Note on that claim procedure |
| **Payment remark** | Optional **Add remark to Open Dental** box at the bottom | Payment-level note (`PayNote`) |

They are independent. You can post line notes without a payment note, or both.

**Example payment remark:** `Cigna remit 8/24 — check posted in Ordo by J. Park`

On **reject**, if you checked the payment-remark box, that text can be stored as a procedure note so the reason for rejecting is not lost. Fill it in if you reject something non-obvious (“wrong year, patient has two Marias in family”).

---

## Approve vs post vs reject

| Action | What it does | Writes to Open Dental? |
| --- | --- | --- |
| **Approve match** | Locks the selected Open Dental claim. | No |
| **Post payment** | Writes `InsPayAmt` and notes. Disabled until approved. | Yes (Actual, when connected) |
| **Reject match** | Discards the match. Unavailable after a successful post. | No |

If Open Dental changed after approve (someone edited the claim in the chair), Ordo asks you to review again instead of overwriting.

After a successful post you should see confirmation, including a claim payment number when the API returns one.

---

## What your role can click

| Permission | Button |
| --- | --- |
| Approve match | **Approve match** |
| Reject match | **Reject match** |
| Post payment | **Post payment** |
| Edit extracted data | Corrections on **EOB Review** |

A Reviewer at Bright Smile can approve and reject but cannot post. Jennifer posts after Mike’s approval. That two-person pattern is optional; Owners can collapse it into one role.

---

## Related pages

- [Finding the patient](finding-the-patient.md)
- [Post a payment](posting-a-payment.md)
- [What each operation does](operations.md)
- [Statuses](statuses.md)
- [Inside an EOB](../modules/working-an-eob.md)
- [When something looks wrong](../examples/when-things-go-wrong.md)
- [Open Dental errors](../errors/open-dental.md)
