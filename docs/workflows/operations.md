# What each operation does

This page is the catalog of **buttons and automatic steps**. For every operation it answers: who can do it, what happens, which **status** changes, and what a success or failure looks like.

If you only need the Monday morning ritual, start with [Post a payment](posting-a-payment.md). Use this page when you want the full picture of a single click.

**Nothing is written to Open Dental until Post payment** (or a reject remark that you chose to send). Approve is not a post.

---

## How to read this page

Each operation has:

| Heading | Meaning |
| --- | --- |
| **Who** | The permission (and typical role) that sees the button. |
| **Writes to Open Dental?** | Whether live charts can change. In Demo the answer is always no. |
| **Status change** | What the file row, patient row, or match status becomes. Full map: [Statuses](statuses.md). |
| **If it fails** | The usual message and the next step. Open Dental API wording: [Open Dental errors](../errors/open-dental.md). |

---

## 1. Sign in

**Who.** Anyone with an account (or the Demo sample user).

**Writes to Open Dental?** No.

**What happens.** You pick **Demo** or **Actual**, then prove who you are (password or email code). Ordo loads the modules your **role** allows.

**Status change.** None on files. You land on the EOB Dashboard if you can see it.

**Success.** The sidebar shows your name, the mode (Demo or Actual), and the modules you can open.

**Typical failures.**

| You see | Meaning |
| --- | --- |
| **Invalid or expired code** | The email code was wrong or too old. Request a new one. |
| **Waiting for access** | You signed up, but no Owner has invited you yet. |
| **No organization found for your account** | Your login is not attached to a practice. Contact Ordo. |

Story: [Sign in](../people/signing-in.md).

---

## 2. Upload EOBs

**Who.** Permission **Upload EOBs** (Owner, Admin by default).

**Writes to Open Dental?** No. The file is stored in Ordo only.

**What happens.**

1. You drop a PDF (or TIFF / PNG / JPEG) on the [EOB Dashboard](../modules/eob-dashboard.md).
2. Ordo saves the file and starts **reading** it (extraction).
3. You wait until the row is **Extracted** or **Failed**.

**Status change (file).**

`Uploaded` → **Queued** → **Extracting** → **Extracted** (ready) or **Failed**.

**Success.** The row shows patient / claim / procedure counts. Example: `Cigna_Remit_Aug24.pdf` → **3 patients, 3 claims, 8 procedures**.

**Typical failures.**

| You see | Meaning |
| --- | --- |
| **You must be signed in to upload** / **Session expired** | Sign in again, then drop the file. |
| **Upload failed** | The file did not save. Try once more; contact Ordo if it repeats. |
| File stays **Extracting** | Reading is still running, or stuck. Refresh; wait a few minutes. |

Accepted types: PDF, TIFF, PNG, JPEG. Reading today understands **Cigna Dental** standard remittances.

---

## 3. Extraction (automatic)

You do not click this. It starts after upload.

**Who.** The system.

**Writes to Open Dental?** No.

**What happens.** Ordo opens the PDF, looks for a Cigna Dental layout, and pulls out patients, claims, procedure codes, and plan covered amounts.

**Status change (file).**

While it runs: **Extracting** (extraction status **Processing**).  
When it finishes: **Extracted** (extraction **Completed**), or **Failed** (extraction **Failed**).

**Success.** Patients appear when you open the file. Extraction does **not** fetch Open Dental. That is a separate click.

**Typical failures.**

| You see | Meaning |
| --- | --- |
| **Unsupported EOB format — expected Cigna Dental standard layout** | This layout is not read yet. Post that check in Open Dental by hand. Archive the failed file so it does not sit in Failed. |
| **No claims extracted** / **Parsed as Cigna Dental but found no claims or procedures** | Layout looked Cigna-ish but no claim lines were found. Re-export a clean PDF from the payer portal. |
| **Could not download EOB file** | The stored file could not be opened. Contact Ordo with the EOB ID. |

A notification such as “extraction finished” or “extraction failed” may appear if your practice enabled it.

---

## 4. Open a file

**Who.** Permission **EOB dashboard** (view).

**Writes to Open Dental?** No.

**What happens.** You click a dashboard row and see the patient list for that remittance.

**Status change.** None. Opening is always safe.

**Success.** You see names, amounts, and a review status on each row.

---

## 5. Fetch Open Dental

This is the most important habit after upload.

**Who.** Anyone who can open the file (you need patients selected).

**Writes to Open Dental?** No. Fetch **reads** charts. It does not post money.

**What happens.**

1. Tick one or more patients.
2. Click **Fetch Open Dental**.
3. In **Actual**, Ordo looks up those names in Open Dental (via the API), copies matching patients / claims / procedure lines into Ordo’s **replica**, then scores claim **candidates**.
4. In **Demo**, Ordo uses sample charts. You still must click Fetch.

**Status change (patient row).**

| Before | After a successful fetch |
| --- | --- |
| **Not fetched** | **Needs review** if candidates exist, **No match** if none, **Failed** if the call errored |

The file stays **Extracted**. Fetch does not change the file-level status.

**Success toast (example).** `Fetched Open Dental for 2 patients` — `2 OD patients · 3 claims`.

**Typical failures.**

| You see | Meaning |
| --- | --- |
| **Nothing new to fetch** | Those patients were already fetched. Use **Refetch** if you need a fresh copy. |
| **Open Dental is not connected…** | An Admin must save the customer key and Test under Clinic settings → Integrations. |
| **No Open Dental patients matched the EOB names** | The replica search found nobody with those names. Check spelling on **EOB Review**, then fetch again. Search Open Dental yourself. |
| **Open Dental fetch failed** / **Open Dental API 401…** | The wire to Open Dental failed. See [Open Dental errors](../errors/open-dental.md). |
| Patient row **Failed** | Fetch recorded an error on that person. Read the remark; retry fetch. |

!!! warning "Do not skip Fetch"
    Opening a patient before Fetch only shows the EOB. The Open Dental tab looks empty. That is expected, not a bug.

You can fetch again later (**Refetch**) if someone just entered a claim in Open Dental and you need a fresh copy.

---

## 6. Refetch Open Dental

**Who.** Same as Fetch.

**Writes to Open Dental?** No.

**What happens.** Same as Fetch, but only for patients that were **already** fetched. Use this after a chart change in Open Dental, or after you edited a name on **EOB Review**.

**Status change.** The patient row is re-scored. An old **Approved** match is **not** automatically undone by refetch — if the chart changed after approve, **Post payment** will stop and ask you to review again.

**Typical failure.** **Nothing to refetch** — you selected people who have never been fetched. Use **Fetch** instead.

---

## 7. Edit extracted data (EOB Review)

**Who.** Permission **Edit extracted data**.

**Writes to Open Dental?** No. You are correcting what Ordo read from the PDF.

**What happens.** On **EOB Review**, you fix a name, date, code, or amount that the reader got slightly wrong.

**Status change.** The extracted fields update. Match status may still say **Pending** or **Needs review** until you **Fetch** (or refetch) so scoring uses the new values.

**Success.** Example: `MARIA SANT0S` (zero) becomes `SANTOS`. After refetch, name similarity rises and Approve may become available.

**Typical failure.** The save did not complete (session or permission). Sign in again. Confirm your role includes edit.

---

## 8. Approve match

**Who.** Permission **Approve match**.

**Writes to Open Dental?** **No.** This only locks the selected Open Dental claim inside Ordo.

**What happens.**

1. On the **Open Dental** tab, you select a candidate (the recommended one is pre-selected when Ordo is confident).
2. You confirm it is not a **Hard mismatch**.
3. You click **Approve match**.
4. Ordo stores a **push package** — a snapshot of the procedure amounts it will write later. Nothing is sent to Open Dental yet.

**Status change.**

| Where | Becomes |
| --- | --- |
| Patient row | **Approved** |
| Match | **Approved** |
| Push package | **Approved** (ready to post) |

**Success toast.** `Match approved` — `Claim 18421 → OD 18421. Nothing posted yet.`

**Typical failures.**

| You see | Meaning |
| --- | --- |
| Button missing | Your role does not include Approve. |
| Button disabled | No candidate, already approved, already posted, or **Hard mismatch**. |
| **Pick a candidate without a hard mismatch** | The selected claim failed identity checks. Open **Audit**, pick another claim, or reject. |
| **Cannot approve a hard-mismatch candidate** | Same rule, from the server. |
| **EOB claim not found. Refetch Open Dental…** | Fetch again, then approve. |
| **That Open Dental claim is no longer a valid match…** | The replica changed. Refetch, then approve again. |
| **Approve failed** | Session, permission, or server. Try once; then contact Ordo. |

---

## 9. Reject match

**Who.** Permission **Reject match**.

**Writes to Open Dental?** Usually **no**. If you tick **Add remark to Open Dental** and type a note, Ordo may write that note onto a procedure (`Note`) so the reason is not lost. The money is still not posted. If that note write fails, the reject in Ordo still succeeds.

**What happens.** The current match is discarded. The patient is not posted.

**Status change.**

| Where | Becomes |
| --- | --- |
| Patient row | **Rejected** |
| Match | **Rejected** |
| Push package (if one was approved) | **Rejected** |

**Success.** Toast `Match rejected`. If you sent a remark: `Remark written to Open Dental` or `Remark saved in Ordo`.

**Typical failures.**

| You see | Meaning |
| --- | --- |
| **Enter a remark, or uncheck Add remark** | You ticked the box but left it blank. |
| **Reject failed** | The Ordo save did not complete. Try once. |
| Unavailable after **Posted** | You cannot reject a successful post. |

---

## 10. Post payment

**Who.** Permission **Post payment**. Disabled until the match is **Approved**. After a successful post it stays available so you can confirm.

**Writes to Open Dental?** **Yes** in Actual when connected. In Demo it is a simulation.

**What happens in Actual (the real write).** Ordo talks to Open Dental in this order:

1. Re-reads the claim procedure lines. If they changed since approve (amount, code, or a line disappeared), it **stops** and asks you to review again.
2. Updates each matched procedure that is **not** already on a check: insurance paid amount (`InsPayAmt`), status **Received**, and your line remark if you typed one. If the line is already on a check with the **same** amount, Ordo skips that write.
3. Marks the claim **Received** (`ClaimStatus` **R**) and sets the date received.
4. Creates an insurance **claim payment** (the check) if one does not already exist, and returns a **claim payment number** when the API does.
5. Double-checks that the amounts now sitting in Open Dental match what Ordo intended.

**Status change.**

| Result | Patient / match | Meaning |
| --- | --- | --- |
| Success (including already posted with the same amounts) | **Posted** | Money is on the claim. Remarks become read-only. **Post payment** stays available. |
| Chart changed, or an attached check has a **different** amount | **Needs review** (match: **push requires review**) | Fetch, read the lines, approve again, post **once**. |
| API / network failure | **Needs review** (match: **push failed**) | Approve again, then post. Check the chart first. |

**Success popup.** `Posted to Open Dental` with `ClaimPaymentNum` when the API returns one, plus the amount. Failed posts open a popup with the error and **View audit** (the patient’s **Audit** tab). Keep the claim payment number if the dentist asks “did it really post?”

**Typical failures.**

| You see | Meaning |
| --- | --- |
| **Open Dental changed since approval** | Someone (or another process) edited the claim after you approved. Do **not** post blindly. Fetch, confirm, approve, post once. |
| **Open Dental is not connected…** | Connect and Test first. |
| **Cannot post payment: Open Dental ClaimNum is missing** | The match snapshot has no claim number. Reject, fetch, approve again. |
| **Push package not found** / **documentId and an approved push package are required** | Approve again, then post. |
| **Post payment failed** / **Push failed** / **Open Dental API 400…** | The write did not finish cleanly. **Look in Open Dental first.** If the money is already there and matches the EOB, you can post again — Ordo will treat it as already posted. If the amount is different, stop and review. Decoder: [Open Dental errors](../errors/open-dental.md). |

!!! note "Post again after Posted"
    **Post payment** stays on after a successful post. That is how you confirm the claim without changing lines that are already on a check. After a **failed** post, approve again before posting.

---

## 11. Archive and restore (file)

**Who.** Permission **Archive**.

**Writes to Open Dental?** No.

**What happens.** **Archive** hides the remittance from Active and from Reports. **Restore** (from the Archived tab) puts it back. Nothing is deleted.

**Status change (file).** **Archived**, or back to its previous working status (usually **Extracted**).

**When to use it.** Duplicate uploads, test files, remittances you will not post.

---

## 12. Archive a patient (not the whole file)

**Who.** Permission **Archive**, on the [Patients](../modules/patients.md) list.

**Writes to Open Dental?** No.

**What happens.** That person drops off the Patients **Active** list. The rest of the remittance stays.

**Status change.** That patient row is archived (overlay). Use this for a duplicate extraction, not for “we posted her.” Posted patients stay posted; archive is about clutter.

---

## 13. Test Open Dental connection

**Who.** Permission **Manage team and roles** (Owner / Admin). Clinic settings → **Integrations**.

**Writes to Open Dental?** No. Ordo only **reads** a small claim list (`GET /claims` with status Sent) to prove the keys work.

**What happens.** Ordo sends your **developer key** (held by Ordo) and **customer key** (your practice) to the Open Dental API.

**Status change.** Connection **tested** (success) or **failed**. Last test is recorded in Audit and API Logs.

**Success toast.** `Connected to Open Dental API`.

**Typical failures.**

| You see | Meaning |
| --- | --- |
| **Add the clinic customer key…** | Paste the practice key, then Test. |
| **The Ordo developer key is not configured…** | Ordo staff must add it under Administrator. Not something a Reviewer can fix. |
| **Connection test failed** / **Open Dental API 401…** | Keys, eConnector, or permissions. See [Open Dental errors](../errors/open-dental.md). |

---

## 14. Save Open Dental connection

**Who.** Manage team and roles.

**Writes to Open Dental?** No.

**What happens.** The customer key and API URL are stored for this clinic. Saving does not replace Test — Test is how you know the key works.

**Success.** Toast such as `Open Dental saved for Bright Smile Dental`.

---

## 15. Sync (refresh the replica)

**Who.** Manage team and roles. Clinic settings → Integrations → **Sync**. (Fetch on a file is a *patient-scoped* sync plus match. This Sync is the clinic-wide refresh.)

**Writes to Open Dental?** No. Read-only copy into Ordo.

**What happens.** Ordo copies patients, claims, and procedure lines it needs for matching. Matching itself still waits until someone clicks **Fetch Open Dental** on a file.

**Status change.** Last sync time and counts update. A failed sync stores an error on the connection (visible on Integrations).

**Success.** Something like `Synced 120 patients, 40 claims`.

**Typical failures.**

| You see | Meaning |
| --- | --- |
| **Open Dental is not connected…** | Save keys and Test first. |
| **Open Dental returned no Sent or Waiting claims** | The office has no claims in those statuses for the sync to copy. Confirm claims exist in Open Dental. |
| **Open Dental sync failed** / **Open Dental API 400…** | eConnector, keys, or timeout. See [Open Dental errors](../errors/open-dental.md). |

Until Sync (or Fetch) has succeeded at least once, matching has nothing to compare against.

---

## 16. Export

**Who.** Anyone who can see the current list (Dashboard, Patients, inside an EOB, Reports depending on the screen).

**Writes to Open Dental?** No.

**What happens.** Downloads the **current** filtered view, not the entire history.

**Status change.** None.

---

## Pocket map — operations vs Open Dental

| Operation | Reads Open Dental | Writes Open Dental |
| --- | --- | --- |
| Upload / extract / edit EOB | No | No |
| Fetch / Refetch / Sync / Test | Yes | No |
| Approve match | No | No |
| Reject match | Only if you send a remark | Note only, not money |
| Post payment | Yes (to verify) | **Yes** — amounts, claim received, claim payment |

---

## Related pages

- [Statuses — what changes when](statuses.md)
- [Open Dental errors](../errors/open-dental.md)
- [Post a payment](posting-a-payment.md)
- [Matching and remarks](matching-and-remarks.md)
- [Clinic settings](../modules/clinic-settings.md)
