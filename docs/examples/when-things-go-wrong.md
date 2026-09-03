# When something looks wrong

Stories and walkthroughs: [When something looks wrong](../examples/when-things-go-wrong.md). For the message catalog and when to contact Ordo, see [Errors and getting help](../errors/index.md).

---

## The Open Dental tab is empty

**What you see.** EOB Review has lines. Open Dental has no claims.

**Usual cause.** You opened the patient before **Fetch Open Dental**.

**What to do.** Go back to the list, tick the patient, click **Fetch Open Dental**, wait, open the patient again.

**Still empty in Actual?** Open Dental may not be connected or synced. An Admin should test the connection under [Clinic settings → Integrations](../modules/clinic-settings.md). In Demo, fetch still needs to be clicked; it uses sample charts, not your office.

---

## The file says Failed

**What you see.** Dashboard tab **Failed**, or the row never becomes Extracted.

**Usual causes.**

- The PDF is not a **Cigna Dental** standard layout (other carriers may not read yet).
- The file is a photograph of a page, a password-protected PDF, or a statement that is not an EOB.
- A temporary reading error.

**What to do.**

1. Open the file if you can and read the error message.
2. Confirm you uploaded the remittance, not an explanation letter or a claim form.
3. Try a clear PDF export from the payer portal, not a phone photo.
4. If it is a non-Cigna format, plan to post that one in Open Dental by hand until that layout is supported. Archive the failed duplicate so it does not sit in Failed forever.

---

## Hard mismatch / Needs review

**What you see.** A banner or status warning; Approve is disabled or looks unsafe.

**What to do.**

1. Open **Audit**. Read the failed signal in plain language.
2. If the date of service is wrong, pick another **candidate** (another visit).
3. If the name is a near miss (married name, hyphen, typo), fix **EOB Review** if you can edit, fetch again, or confirm in Open Dental which chart is correct.
4. If it is simply the wrong person, **Reject match**. Do not approve because the dollars look close.

**Example.** EOB says June 12. Recommended claim is July 3 (a second cleaning). Dollars might even match. That is still the wrong visit. Pick June 12 or reject.

---

## No match

**What you see.** Status **No match**. Candidate list empty or unusable.

**Usual causes.** Claim was never entered in Open Dental, patient is under a different name, replica is stale (not synced), or the EOB patient is not this practice’s patient.

**What to do.** On the Open Dental tab, use **Find possible patients** (date of birth and similar names) or **None of these are the correct patient** for a manual search. You do not have to edit the EOB name first. Guide: [Finding the patient](../workflows/finding-the-patient.md). If the **claim** exists under that chart, **Sync** (Admin) and fetch again. If the claim does not exist, enter it in Open Dental first, then return to Ordo. Ordo cannot invent a chart.

---

## Post payment failed

**What you see.** Error toast; status may be failed or retry; Maria is not Posted.

**What to do.**

1. Do not hammer the button.
2. Note the time. Open **Clinic settings → API Logs** (or the error panel on the Open Dental tab).
3. Common human fixes: connection dropped, customer key expired, eConnector stopped, claim was locked or already had a check in Open Dental after approve.
4. If Ordo says the claim changed, **review again** (fetch, confirm lines, approve, then post once).
5. If a payment number never appeared but Open Dental already shows the money, **stop**. Email **[help@perfect.ventures](mailto:help@perfect.ventures)** before posting twice.

The full decoder for `Open Dental API 400` (and 401, 429, 504) is [Open Dental errors](../errors/open-dental.md).

---

## I cannot see a button or a module

**Usual cause.** Your **role**. Viewers cannot post. Reviewers cannot post (by default) and cannot open Clinic settings.

**What to do.** Ask an Owner to check [Roles](../people/roles.md). Do not use someone else’s login.

If the whole clinic cannot sign in, the practice may not be set up yet. Email **[help@perfect.ventures](mailto:help@perfect.ventures)**.

---

## Reports look too high or too low

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Uploads doubled | Same PDF uploaded twice | Archive the duplicate file |
| Posted looks low | Files still Approved, not Posted | Finish posting, or check Failed |
| Today’s uploads is zero | Date filter is not today | Change the date preset |
| A file vanished from Reports | It was **Archived** | Restore from Dashboard → Archived if that was a mistake |

Reports use **upload date**, not date of service. June treatment uploaded in August counts in August.

---

## Demo vs Actual mix-up

**What you see.** The file you uploaded this morning is gone — or a sample Maria is still there after you “deleted” her.

**What to do.** Read the sidebar: **Demo** and **Actual** are different cabinets. Switch to the mode you used when you uploaded. Never drop a real EOB in Demo.

---

## Names and PHI on screenshots

If you need help from Ordo, email **[help@perfect.ventures](mailto:help@perfect.ventures)**. Please provide:

- EOB ID (from the dashboard row)
- Time of the error
- The **message text**, not a full-page screenshot of the PDF

Do not paste entire remittances into an unencrypted chat or email.

---

## Related pages

- [Errors and getting help](../errors/index.md)
- [Open Dental errors](../errors/open-dental.md)
- [What each operation does](../workflows/operations.md)
- [Statuses](../workflows/statuses.md)
- [Inside an EOB](../modules/working-an-eob.md)
- [Matching and remarks](../workflows/matching-and-remarks.md)
- [Finding the patient](../workflows/finding-the-patient.md)
- [Clinic settings](../modules/clinic-settings.md)
- [A typical Monday morning](typical-morning.md)
