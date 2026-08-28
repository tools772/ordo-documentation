# Statuses — what changes when

Statuses describe **where the work is**, not whether anyone did a bad job. Ordo shows status in three places that people mix up:

1. **The file** (EOB Dashboard row) — did we read the PDF?
2. **The patient** (inside a file, or on Patients) — did we fetch, approve, post?
3. **The match** (Open Dental tab) — is this claim locked, posted, or stuck?

A file can be **Extracted** while Maria is still **Not fetched** and James is already **Posted**. That is normal: the file is the envelope; the people inside it move at different speeds.

---

## The happy path (one patient)

```
Upload PDF
    → file: Uploaded → Queued → Extracting → Extracted

Tick Maria, Fetch Open Dental
    → Maria: Not fetched → Needs review  (or No match)

Approve match
    → Maria: Needs review → Approved

Post payment
    → Maria: Approved → Posted
```

If you **Reject match**, Maria becomes **Rejected** instead of Approved. The file stays **Extracted**.

---

## File statuses (EOB Dashboard)

These are the words on the **file** row and on the dashboard tabs.

| You see | What it means | What you do |
| --- | --- | --- |
| **Uploaded** | The file arrived. Reading has not finished. | Wait. |
| **Queued** | Waiting its turn to be read. | Wait. Refresh if it sits here a long time. |
| **Extracting** | Ordo is reading the PDF right now. | Wait. Do not post from this file yet. |
| **Extracted** | Patients and lines are ready. | Open the file. Fetch, review, post. |
| **Failed** | Reading (or a rare later file-level error) did not succeed. | Open the row, read the message. See [Errors](../errors/index.md). |
| **Archived** | Hidden from Active and from Reports. Not deleted. | Restore if that was a mistake. |
| **Retry required** | Try the failed step again after the underlying problem is fixed. | Read the message; often a post or connection issue. |

Older or internal labels you might hear from support (same idea, different word):

| Internal name | On screen |
| --- | --- |
| `uploaded` / `queued` / `extracting` | Uploaded / Queued / Extracting |
| extraction `completed` | **Extracted** |
| `failed` | Failed |
| `archived` | Archived |

!!! note "Review is not a file status"
    **Needs review**, **Approved**, and **Posted** live on the **patient**, not on the envelope. The dashboard “Pending review” card is a count of work still to do, not a file-row label.

### What moves the file

| Operation | File status |
| --- | --- |
| Upload | Uploaded → Queued → Extracting |
| Extraction succeeds | **Extracted** |
| Extraction fails | **Failed** |
| Archive | **Archived** |
| Restore | Back to Active (usually Extracted) |
| Fetch / Approve / Post | **Does not change the file row** |

**Example.** Jennifer uploads Monday’s Cigna. The row goes Extracting, then Extracted. Mike fetches and posts all three patients. The dashboard still says **Extracted** on the file — that is correct. Posted is a *person* status. Reports still count the posted payments.

---

## Patient statuses (inside an EOB)

These are the badges on each **person** in the file.

| You see | What it means | Typical next step |
| --- | --- | --- |
| **Not fetched** | You have not clicked **Fetch Open Dental** for this person. | Tick the row, Fetch, then open. |
| **Pending** | Matching has not produced a decision yet (rare on a fetched row). | Fetch if you have not; otherwise open the patient. |
| **Needs review** | Candidates exist, or identity checks need a person. | Open **Open Dental** and **Audit**. |
| **Approved** | Someone confirmed the Open Dental claim. Money is **not** posted. | Someone with Post payment clicks **Post payment**. |
| **Posted** | Payment is in Open Dental (or simulated in Demo). | Done with this person on this file. |
| **Rejected** | Match was thrown away. | Another candidate, post by hand in Open Dental, or leave it. |
| **No match** | Fetch ran; no plausible Open Dental claim. | Search the chart; Sync; enter the claim in Open Dental if it was never charted. |
| **Failed** | Fetch (or a later Open Dental call for this person) errored. | Retry Fetch. Check API Logs. |

### What moves the patient

| Operation | Patient status |
| --- | --- |
| Open file (no fetch) | Stays **Not fetched** |
| Fetch finds claims | **Needs review** (unless already approved/posted/rejected) |
| Fetch finds nobody | **No match** |
| Fetch API error | **Failed** |
| Approve match | **Approved** |
| Post succeeds | **Posted** |
| Post: chart changed | Back toward **Needs review** (see match status below) |
| Post: API failed | **Needs review** with a failed-post flag on the match |
| Reject match | **Rejected** |

**Posted**, **Approved**, and **Rejected** win over fetch: refetching Maria after she is Posted does not take her back to Needs review.

**Example.** Mike fetches Maria and James. Maria becomes Needs review. James is No match (no chart claim). Mike approves Maria. Jennifer posts Maria → Posted. James is still No match until someone charts the visit in Open Dental and Mike fetches again.

---

## Match statuses (Open Dental tab)

These describe **this EOB claim vs that Open Dental claim**. You see them as banners, disabled buttons, and toasts more than as a second badge.

| Status | Meaning | Approve? | Post? |
| --- | --- | --- | --- |
| **Candidate found** | Ordo listed claims. You still pick and confirm. | If not hard mismatch | No |
| **Needs manual** | Ordo wants a person (ambiguous or flagged). | After you pick a safe candidate | No |
| **Approved** | Claim locked in Ordo. Snapshot taken. | Already done | **Yes** |
| **Posted** | Write succeeded. Remarks read-only. | No | Already done |
| **Rejected** | Match discarded. | Start over (fetch / pick again) | No |
| **Push failed** | Post was attempted; Open Dental (or the network) did not finish cleanly. | Do not approve-and-hammer. Check the chart. | Only if Open Dental has **no** payment yet |
| **Push requires review** | The chart changed after approve (line gone, code changed, or amount already sitting there). | Fetch, confirm, approve again | After a new approve |

### Hard mismatch (not a status, a flag)

A candidate can be **Hard mismatch** while the patient is still **Needs review**. Identity failed (patient, date of service, or zero procedure overlap). **Approve is disabled** for that candidate. Pick another claim or reject.

---

## Line statuses (procedure table)

On the Open Dental tab, each EOB line has its own **Status** column. That is not the patient badge.

| Line status | Meaning |
| --- | --- |
| **Match** | The CDT code mapped to an Open Dental claim procedure. |
| **Differs** / **Not matched** | No matching Open Dental procedure on this claim. |

After a successful **Post payment**, remarks freeze (read-only).

---

## Open Dental’s own statuses (what Ordo writes)

You do not set these by hand in Ordo. They matter when you look at the chart after a post, or when API Logs mention them.

### Claim status (the whole visit)

Open Dental uses a letter. After a successful post, Ordo sets the claim to **Received**.

| Code | Word | Meaning in the office |
| --- | --- | --- |
| **U** | Unsent | Not sent to insurance yet. |
| **H** | Hold until primary received | Waiting on another plan. |
| **W** | Waiting in queue | In the send queue. |
| **S** | Sent | Sent to the payer. |
| **R** | Received | Insurance payment recorded. **This is what Ordo sets on post.** |
| **I** | Hold for in process | Held in the office workflow. |

### Procedure (ClaimProc) status

| Word Ordo sends | Meaning |
| --- | --- |
| **NotReceived** | Estimate / not paid yet. |
| **Received** | Insurance paid amount is on this line. **This is what Ordo sets on post** (unless the line is already attached to a check — then Ordo does not change status, only amounts if still allowed). |
| **Supplemental** | Extra payment after the first receive. |
| **Estimate** / **Adjustment** / capitation types | Special rows Ordo does not treat as a normal EOB line to post. |

If Open Dental says the line is already attached to a check, it will **refuse** a new `InsPayAmt`. That is a common **400** on post. See [Open Dental errors](../errors/open-dental.md).

---

## Connection and sync statuses

On **Clinic settings → Integrations**:

| You might see | Meaning |
| --- | --- |
| Connected, last sync time, patient/claim counts | Replica is usable for Fetch. |
| Last sync **failed** plus an error | Sync did not finish. Test the connection; read API Logs. |
| Not connected | Fetch in Actual cannot load live charts. |

Test connection does not change patient rows. It only proves the keys.

---

## Worked example — Maria Santos, one Monday

**File:** `Cigna_Remit_Aug24.pdf`

| Time | What someone did | File | Maria |
| --- | --- | --- | --- |
| 8:07 | Jennifer uploads | Extracting → Extracted | Not fetched |
| 8:12 | Mike ticks Maria, Fetch | Extracted | Needs review |
| 8:14 | Mike approves claim 18421 | Extracted | Approved |
| 8:18 | Jennifer posts | Extracted | Posted |

James Lee on the same file stays **No match** the whole morning. The file never becomes “Posted” as a whole — and that is fine.

---

## Related pages

- [What each operation does](operations.md)
- [Open Dental errors](../errors/open-dental.md)
- [Inside an EOB](../modules/working-an-eob.md)
- [Word list](../glossary.md)
