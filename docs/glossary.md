# Word list

Everyday language for the terms you will see in Ordo. You can skip this page and come back when a label on screen is unclear.

**Ordo** (the product name) comes from Latin: order, row, series, or methodical arrangement — related to the modern English word **system**. See [Where the name comes from](origination.md).

---

## Documents and money

**EOB (Explanation of Benefits)**  
The PDF (or image) the insurance company sends after they process claims. It lists patients, procedure codes, and how much the plan paid. In Ordo, one uploaded file is one EOB — even if that file contains twenty patients.

**Download EOB**  
Saves the original uploaded remittance (PDF or image) to your computer. Available from the Dashboard row menu and from inside a file. This is not the same as **Export**, which downloads a spreadsheet of the current list.

**EOB History**  
On a patient’s detail page, every remittance Ordo has for that person — not just the file you opened last.

**Remittance**  
Another word for the same insurance payment document. People say “today’s remittance” the way they say “today’s EOB.”

**Plan covered amount**  
The dollars on the EOB that Ordo will post as the insurance payment. It is not always the same as the dentist’s billed fee, the patient’s copay, or the write-off.

**InsPayAmt**  
Open Dental’s field name for “insurance paid amount.” When you click **Post payment**, Ordo writes the EOB plan covered amount into this field. You do not need to memorize the name; the screen labels it in friendlier words.

**Claim payment / claim payment number**  
After a successful post, Open Dental may return a payment number. Ordo shows it as confirmation that the write happened.

---

## People and claims

**Patient**  
A person extracted from the EOB. In Ordo they appear both inside a file and on the cross-file **Patients** list.

**Subscriber**  
The person whose insurance policy it is. Often the patient; sometimes a parent or spouse. Subscriber ID is a strong clue when matching to Open Dental.

**Claim**  
One visit (or one billing package) sent to insurance. An EOB can list several claims for the same patient, or one claim with several procedure lines.

**Procedure line**  
One row on the claim: a CDT code (for example D1110, a cleaning), a date of service, and amounts.

**CDT code**  
The American Dental Association procedure code. D0150 is a comprehensive exam. D1110 is an adult prophylaxis (cleaning). Ordo matches EOB lines to Open Dental using these codes.

**Date of service (DOS)**  
The day the dentistry was actually done. Matching uses this date. A claim for June 12 will not happily match a claim for July 3.

**Carrier / payer**  
The insurance company (Cigna, Delta, and so on).

---

## Matching and posting

**Match**  
Ordo’s guess (or your confirmation) that “this EOB claim is that Open Dental claim.”

**Fetch Open Dental**  
The button that loads chart data from the practice’s Open Dental copy so you can compare. Until you fetch, the Open Dental tab is empty or EOB-only.

**Candidate**  
One possible Open Dental claim Ordo is offering you. The recommended row is pre-selected when Ordo is confident.

**Hard mismatch**  
A serious identity problem: the patient, date of service, or procedure codes do not line up. Do not approve these until you pick a better claim or reject.

**Approve match**  
Locks in the Open Dental claim you selected. **Does not post money.**

**Post payment**  
Writes the amounts (and optional notes) to Open Dental. Stays off until the match is **Approved**. After **Posted** it stays off.

**Workflow guide**  
An in-app button on the EOB patient list that maps which actions are allowed at each status. The longer version is [Statuses](workflows/statuses.md).

**Reject match**  
Throws away the current match without posting. Use this when the recommended claim is the wrong visit.

**Remark**  
A short note. There are two kinds:

- **Procedure remark** — on each line (starts as “Match” or “Not matched”). Becomes a note on that Open Dental procedure when you post.
- **Payment remark** — the optional box at the bottom of the card. Becomes a note on the whole payment.

**Audit**  
On a patient: Open Dental API calls for this EOB, plus the checklist of comparisons (patient ID, name, date of service, procedures, amounts). Open this tab when a match looks “off” or a post failed.

**Signal**  
One row on that checklist. A failed signal is Ordo saying “these two values are not the same.”

---

## Status words you will see

Statuses describe **where work is**, not whether anyone did a bad job.

| You might see | Plain meaning |
| --- | --- |
| Uploaded | The file arrived. Reading has not finished. |
| Queued | Waiting its turn to be read. |
| Extracting / Processing | Ordo is reading the PDF. |
| Extracted / Ready | Patients and lines are available to review. |
| Not fetched | This person has not had **Fetch Open Dental** yet. |
| Needs review | A person should look. Matching was unsure or flagged. |
| Approved | Someone confirmed the Open Dental claim. Not posted yet. |
| Posting | The write to Open Dental is in progress. |
| Posted / Completed | The payment is in Open Dental. |
| Failed | Reading, fetch, or posting did not succeed. Open the file or logs. |
| Retry required | Try again after the underlying problem is fixed. |
| Archived | Hidden from the active inbox and from Reports. Not deleted. |
| Pending | Not fetched yet, or matching has not produced a decision. |
| No match | Ordo could not find a plausible Open Dental claim. |
| Rejected | Someone threw away the match without posting. |
| Matched | A candidate was found; you still review before posting. |
| Hard mismatch | Identity failed on this candidate. Do not approve it. |
| Open Dental API 400 / 401 / 429 / 504 | Open Dental refused or timed out. See [Open Dental errors](errors/open-dental.md). |

On the **Patients** list, filters such as Pending, Needs review, Matched, No match, and Archived refer to that person’s match status across files.

The full lifecycle (file vs patient vs match): [Statuses](workflows/statuses.md). Each button: [What each operation does](workflows/operations.md).

---

## Practice and access

**Role**  
A named bundle of permissions: Owner, Admin, Reviewer, Viewer, or a custom role your clinic created. Roles decide which modules and buttons you see.

**Permission**  
One specific ability, such as “Upload EOBs” or “Post payment.”

**Organization / clinic / practice**  
Your dental office in Ordo. Multi-location practices can also have **locations** and map users to them.

**Allowlist**  
The list of people or clinics allowed into the product. If someone cannot sign in, they may not be on the allowlist yet. Ask your office manager to email **[help@perfect.ventures](mailto:help@perfect.ventures)**.

**API logs**  
A technical diary of calls to Open Dental. Useful when a connection test or post fails. How to read the numbers: [Open Dental errors](errors/open-dental.md). Most billing staff will rarely need this; office managers might, with Ordo support at **[help@perfect.ventures](mailto:help@perfect.ventures)**.

**eConnector**  
The Open Dental service at the office that lets the cloud API reach your charts. If it is not running, Test, Fetch, and Post fail with a 400-style message.

**ClaimProc**  
Open Dental’s name for one insurance line on a claim (the row that holds `InsPayAmt`). Ordo posts onto ClaimProcs.

**ClaimPayment / ClaimPaymentNum**  
The insurance check record in Open Dental. After a successful post, Ordo shows this number as confirmation.

**Audit log**  
A people-oriented diary: who uploaded, who approved, who posted. This is the log to open when you need “who did what, when.”

---

## Systems Ordo talks to

**Open Dental**  
The practice management system (charts, claims, ledgers). Ordo does not replace it. Ordo posts *into* it.

**Replica / sync**  
Ordo keeps a local copy of some Open Dental data so matching is fast. **Fetch** and **Sync** refresh that copy. If Open Dental changed after you approved, Ordo will ask you to review again instead of silently overwriting.

**PMS**  
“Practice management system” — for Ordo today, that means Open Dental.
