# Errors and getting help

When Ordo cannot finish a step, it shows a **status** (Failed, Needs review, No match) and often a **short message**. This page is the decoder ring: what that usually means, what you can try, and when to stop and **reach out to Ordo**.

The one rule: after a **Post payment** failure, **look in Open Dental first**, then use this page. If the payment already matches the EOB, posting again is allowed. If the amount is different, fetch and review before you approve again.

Stories and walkthroughs: [When something looks wrong](../examples/when-things-go-wrong.md). Open Dental HTTP codes and posting refusals: [Open Dental errors](open-dental.md). What each button changes: [Operations](../workflows/operations.md) and [Statuses](../workflows/statuses.md).

---

## How to read an error

| Where it appears | What it is |
| --- | --- |
| Red or amber **toast** (corner of the screen) | A one-line message for Fetch, Approve, Reject, Test, and similar. |
| **Popup** after Post payment | Success (ClaimPaymentNum and amount) or the error, with **View audit**. |
| File status **Failed** on the EOB Dashboard | Ordo could not read the PDF, or a later step failed for that file. |
| Patient status **Needs review**, **No match**, **Hard mismatch** | Matching needs a person. Not always a product bug. |
| **Audit** tab | Open Dental API calls for this EOB, plus each failed **signal** (name, date, codes, amounts). |
| **API Logs** (Clinic settings) | Clinic-wide diary of calls to Open Dental. |

**Example.** Jennifer posts Maria Santos. A popup says `Open Dental changed since approval`. That is not “Ordo is down.” It means the chart changed after Mike approved. She fetches again, checks the lines, approves, and posts once.

---

## What you can try vs when to contact us

Try it yourself when:

- You skipped **Fetch Open Dental**
- The PDF is the wrong kind of file (photo, statement, non-Cigna layout)
- The recommended claim is the wrong visit
- You are in **Demo** instead of **Actual** (or the reverse)
- Your role does not include that button
- Reports look wrong because of filters or a duplicate upload

**Contact Ordo** when:

- The same failure happens after one careful retry
- Posting may have written money **and** still showed an error (risk of a double post)
- The whole clinic cannot sign in
- Open Dental connection test fails after the customer key is saved
- A Cigna PDF that used to work suddenly always fails
- You are not sure whether the payment landed in Open Dental

---

## Common messages

Each row: what you see, why it happens, what to do, and whether you need us.

### Upload and reading

| You see | Why | What you can do | Need Ordo? |
| --- | --- | --- | --- |
| **Unsupported EOB format** / expected Cigna Dental layout | The reader today understands **Cigna Dental** standard remittances. Other carriers or layouts are not parsed. | Confirm it is a Cigna remittance PDF from the payer portal, not a photo or a claim form. Post that check in Open Dental by hand if it is another carrier. Archive the failed file so it does not clutter Failed. | **Yes**, if it *is* a standard Cigna Dental EOB and still fails — send the EOB ID and time. |
| **No claims extracted** | Ordo recognized Cigna-ish layout but found no claim/procedure lines. | Re-export a clean PDF. Do not scan a printout at an angle. | **Yes**, if a normal Cigna remittance comes out empty. |
| **You must be signed in to upload** / **Session expired** | The login timed out. | Sign in again, then upload. | No, unless it happens immediately after a fresh sign-in. |
| **Could not reach the server** | Network, VPN, or Ordo is briefly unreachable. | Check internet, try once more. | **Yes**, if it lasts more than a few minutes for the whole office. |
| File stays **Extracting** for a long time | The job is queued or stuck. | Refresh the dashboard. Wait a few minutes. | **Yes**, if it never becomes Extracted or Failed. |

### Matching (Open Dental tab and Audit)

| You see | Why | What you can do | Need Ordo? |
| --- | --- | --- | --- |
| Open Dental tab is empty | You opened the patient **before Fetch Open Dental**. | Select the patient, click **Fetch Open Dental**, then open the row. | No, unless Fetch itself errors. |
| **Hard mismatch** / Approve disabled | Identity checks failed (patient, date of service, or procedure codes). Dollars can still add up. | Open **Audit**. Pick another claim candidate, or **Reject match**. Do not approve a hard mismatch. | No for a wrong visit. **Yes** if every candidate on a clearly correct patient is hard-mismatch. |
| **Patient name mismatch — EOB has … Open Dental has …** | Names differ (married name, typo, extra hyphen). | Confirm the chart. Edit extracted name if your role allows, then fetch again. | No, unless the names are clearly the same person and Audit still blocks everything. |
| **Date of service** mismatch | Recommended claim is a different visit (two cleanings in one month). | Pick the claim with the EOB date. | No. |
| **No match** | No plausible Open Dental claim in the replica. | Search Open Dental. Sync (Admin), fetch again. Enter the claim in Open Dental if it was never charted. | **Yes** if the claim is sitting in Open Dental and Fetch/Sync still cannot see it. |
| **Pick a candidate without a hard mismatch** | You tried to approve a flagged claim. | Choose a different candidate or reject. | No. |

### Approve and post

| You see | Why | What you can do | Need Ordo? |
| --- | --- | --- | --- |
| **Approve failed** / **Reject failed** | The save did not complete (session, permission, or server). | Sign in again. Confirm your role includes Approve/Reject. Try once. | **Yes** after one retry. |
| **Enter a remark, or uncheck Add remark** | You ticked the payment-remark box but left it blank. | Type a note or untick the box. | No. |
| **Pick a candidate without a hard mismatch** / **Cannot approve a hard-mismatch candidate** | Identity checks failed on the selected claim. | Open Audit. Pick another claim or reject. | No. |
| **That Open Dental claim is no longer a valid match** | The replica changed after you loaded candidates. | Refetch, then approve again. | No. |
| **Open Dental changed since approval** | Someone edited the claim in Open Dental after you approved (line gone, code changed, or amount already there). Ordo will not overwrite quietly. | Fetch, read the lines, approve again, then post **once**. | No, unless it repeats every time with nobody editing the chart. |
| **ClaimProc … already has InsPayAmt** / **Verify failed for ClaimProc** | The chart already has money on that line, or the write did not stick. | Look in Open Dental. If it matches the EOB, you can post again. If it differs, fetch and review. | **Yes immediately** if you are unsure. |
| **InsPayAmt cannot be updated once the procedure is attached to a check** | Open Dental already has a check on that line. | Open the chart. If the amount matches the EOB, post again. If it differs, fetch and review. | **Yes** if you did not expect a check to be there. |
| **Post payment failed** / **Push failed** / **Open Dental API 400/401/429/504** | The write to Open Dental did not finish (connection, key, locked claim, eConnector, rate limit, or a business rule). | Check Open Dental. If the money matches the EOB, post again. If not, approve again only after you know. Decoder: [Open Dental errors](open-dental.md). | **Yes immediately** if you are unsure. |
| Success popup with a **claim payment number** | The write worked. | You are done with that patient on this file. **Post payment** is off. | No. |

### Sign-in, roles, and connection

| You see | Why | What you can do | Need Ordo? |
| --- | --- | --- | --- |
| **Invalid or expired code** | Email code was wrong or too old. | Request a new code. Check spam. | No, unless codes never arrive. |
| Missing **Post payment** or **Upload** | Your **role** does not include that permission. | Ask an Owner to change the role. Do not share logins. | No. |
| Whole clinic cannot sign in | Practice not set up, inactive users, or access turned off. | One Owner tries a password reset. | **Yes** — this is Ordo-side access. |
| **Connection test failed** / **Open Dental sync failed** | Customer key, API URL, eConnector, or Open Dental API rejected the call. | Admin: confirm the customer key, Test, then Sync. See API Logs. | **Yes** if Test still fails with a saved, current key. |
| **Open Dental API 401** | Keys invalid, unassigned, or disabled. | Re-save the customer key. Test. Do not paste keys into chat. | **Yes** if the key is current and Test still fails. |
| **Open Dental API 429** / **504** | Too many requests queued, or the office took longer than 60 seconds. | Wait, then retry **once**. If this was Post, check the chart first. | **Yes** if it keeps happening. |
| **eConnector is not running** | The office connector service is stopped. | IT / Open Dental: start eConnector, then Test in Ordo. | Yes if you cannot start it. |
| **No organization found for your account** | The user is not attached to a practice. | Do not keep signing up. | **Yes**. |

---

## Reach out to Ordo

If the table says **Need Ordo? Yes**, or if you need help with any issue, email our dedicated support group at **[help@perfect.ventures](mailto:help@perfect.ventures)**.

Do **not** paste the full EOB PDF or a screenshot of patient names into a group chat or unencrypted email.

Send this instead (copy and fill in):

```
To: help@perfect.ventures
Subject: [Ordo Issue] <Short summary>

What I was doing:
What I saw (copy the exact message):
EOB ID (from the dashboard row):
Patient name as shown in Ordo (if needed):
Time (your timezone):
App mode (Demo or Actual):
Did I already click Post payment? (yes/no)
Did Open Dental already show the insurance payment? (yes / no / not sure)
```

If posting might have happened twice, say that in the first sentence. We would rather check the ledger with you than have you click Post again.

---

## Related pages

- [Open Dental errors](open-dental.md) — HTTP codes, posting refusals, API Logs
- [What each operation does](../workflows/operations.md)
- [Statuses](../workflows/statuses.md)
- [When something looks wrong](../examples/when-things-go-wrong.md) — short scenes
- [Matching and remarks](../workflows/matching-and-remarks.md)
- [Clinic settings](../modules/clinic-settings.md)
- [Roles and who can do what](../people/roles.md)
