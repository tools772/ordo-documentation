# Open Dental errors

When Ordo talks to **Open Dental**, a failure often arrives as a toast plus a row in **Clinic settings → API Logs** (and the **Open Dental errors** card on Integrations). This page translates those messages into office language.

The one rule after a **Post payment** failure: **look in Open Dental first.** If the insurance payment is already on the claim, **stop**. Do not click Post again. Contact Ordo.

Stories: [When something looks wrong](../examples/when-things-go-wrong.md). Other Ordo messages (upload, matching, sign-in): [Errors and getting help](index.md).

---

## Where the message appears

| Place | What it is |
| --- | --- |
| Red **toast** | The action you just took (Test, Fetch, Sync, Post, Reject). |
| Patient row **Failed** | Fetch for that person did not complete. |
| Match banner **Open Dental post failed** / **Open Dental changed since approval** | Post was attempted. |
| **API Logs** | One row per HTTP call: method, path (for example `PUT /claimprocs/293`), status code, body. |
| **Open Dental errors** card | Failed calls only — copy this when you write to Ordo. |
| **Audit** | Human history (`Open Dental post failed`, sync completed, connection tested). |

A toast often starts with `Open Dental API 400:` (or 401, 404, …) and then Open Dental’s own explanation. The number is an **HTTP status**. The text after the colon is Open Dental (or the eConnector) talking.

**Example.** Jennifer posts Maria. Toast: `Open Dental API 400: InsPayAmt cannot be updated once the procedure is attached to a check.` That means Open Dental already has a check on that line. She opens the chart, sees the payment, and does **not** post again.

---

## How to read an API Logs row

| Column | Plain meaning |
| --- | --- |
| **Method** | `GET` = reading. `PUT` = updating a line or claim. `POST` = creating a claim payment (the check). |
| **Endpoint** | What Open Dental object: `/claims`, `/claimprocs/123`, `/claimpayments`, `/patients`. |
| **Status** | `200` or `201` = Open Dental accepted it. Anything else is a problem (or a timeout recorded as `0`). |
| **Error / response** | The explanation. Copy this into an email to Ordo. |

### Which call is which operation

| You clicked | Typical Open Dental calls |
| --- | --- |
| **Test** | `GET /claims?ClaimStatus=S` (Sent claims — a cheap “are you there?”) |
| **Sync** (clinic-wide) | `GET` patients, claims, claimprocs, carriers, plans, providers |
| **Fetch Open Dental** | `GET /patients` by name, then claims and claimprocs for those patients |
| **Post payment** | `PUT /claimprocs/{number}` (each line) → `PUT /claims/{number}` → `POST /claimpayments` |
| **Reject** with a remark | `GET /claimprocs` then `PUT /claimprocs/{number}` with a **Note** only |

---

## HTTP status codes from Open Dental

These are the codes Open Dental documents for its API. Ordo shows them as `Open Dental API {code}: …`.

| Code | Open Dental’s name | What it usually means in the office | What you can do |
| --- | --- | --- | --- |
| **200** | OK | Read or update succeeded. | Nothing — this is success. |
| **201** | Created | A new claim payment (check) was created. | You should see a **ClaimPaymentNum** in the success toast. |
| **400** | Bad request | Open Dental refused the request. Common causes: **eConnector** not running (or two eConnectors fighting over the same registration key), the office **version** is too old for this method, a **timeout** on the way to the office, missing headers, **or a business rule** (line already on a check, amounts do not add up, claim payment batch-only preference). | Read the text after the colon. Table below. Test the connection. If posting, check the chart before retrying. |
| **401** | Unauthorized | **Customer key** or **developer key** is wrong, unassigned, or disabled — or the developer key is not allowed to use that method. | Admin: confirm the customer key, Test. If it still fails, Ordo + Open Dental support (do not paste keys in chat). |
| **404** | Not found | That patient, claim, or procedure number does not exist (deleted, wrong id) — or the URL is wrong. | Fetch again. If the claim was deleted in Open Dental, you cannot post it; enter a new claim in Open Dental first. |
| **410** | Gone | That API method was retired. | Contact Ordo — this is a product/version issue, not something to retry. |
| **429** | Too many requests | Too many calls are queued for **this practice’s customer key**. Open Dental processes them one at a time. The response may include **Retry-After**. | Wait a minute. Do not click Fetch/Post in a loop. Try once. |
| **504** | Gateway timeout | The request did not finish in **60 seconds** (office server busy, or too much data). | Wait, Test, then retry **once**. If this was Post, check Open Dental before posting again. |
| **0** (in logs) | No HTTP status | Network error before a response (VPN, DNS, Ordo could not reach `api.opendental.com`). | Check internet. Try Test. Contact Ordo if the whole office is down. |

---

## Messages Open Dental often sends (and what they mean)

Open Dental usually adds a short **explanation** with 400 and 404. The wording can vary by version. Match the **idea**, not every comma.

### Keys, eConnector, and “we cannot reach the office”

| You might see (idea) | Meaning | What to do |
| --- | --- | --- |
| eConnector is not running | The office program that connects Open Dental to the cloud API is stopped. | On the server that runs Open Dental services, start **eConnector**. Then Test in Ordo. |
| Two eConnectors … same registration key | Two machines are registered as the connector. Open Dental will refuse work until that is cleaned up. | Open Dental support / your IT person. Not an Ordo posting bug. |
| Version … not high enough | The practice’s Open Dental build is older than the API method Ordo is calling. | Update Open Dental (or ask your vendor). Contact Ordo if you cannot update yet. |
| Invalid credentials / unauthorized / key disabled | Customer or developer key is wrong or turned off. | Re-save the customer key. Test. Rotate the key in Open Dental if it leaked. |
| Request timeout / connectivity | The hop from Open Dental’s cloud to **your** office failed. | Confirm the office is online, eConnector is running, then Test. |

**Example.** Test fails with `Open Dental API 400:` and a mention of eConnector. Jennifer does not re-type the customer key ten times. She asks IT whether eConnector is running on the server, then Tests once.

### Fetch, sync, and patients

| You might see | Meaning | What to do |
| --- | --- | --- |
| Patient not found / 404 on `/patients/…` | That PatNum is gone. | Fetch by name again; the replica may be stale. |
| **No Open Dental patients matched the EOB names** (Ordo) | Search by first/last name returned nobody. | Fix spelling on EOB Review, fetch again. Confirm the patient exists in Open Dental. |
| **Open Dental returned no Sent or Waiting claims** (Ordo, clinic Sync) | Clinic-wide sync looks for claims in Sent or Waiting and found none. | Confirm claims exist. Fetch on a specific patient still searches that person. |
| **No matching patients found for this document** (Ordo) | Fetch was called with patient ids that are not on this file. | Re-select patients on the list, Fetch again. |

### Posting — procedure lines (`PUT /claimprocs/…`)

This is the first write during **Post payment**. Open Dental treats claim procedures as delicate.

| You might see (idea) | Meaning | What to do |
| --- | --- | --- |
| **InsPayAmt cannot be updated once the procedure is attached to a check** | That line already has a **ClaimPayment** (a check). Open Dental will not let Ordo change the paid amount. | Open the claim in Open Dental. If the payment is already there, **stop**. If a *different* check is attached, this visit cannot be posted through Ordo until that is sorted in Open Dental. |
| Cannot update a ClaimProc that **IsTransfer** is true | This row is an income transfer, not a normal insurance line. | Do not post this candidate. Pick another claim or post by hand. |
| Cannot update status **Adjustment**, **InsHist**, **CapClaim**, **CapComplete**, **CapEstimate** | That row type is not a receivable claim line Ordo can receive. | Wrong claim or a capitation/adjustment row. Reject or handle in Open Dental. |
| ClaimProc not found (404) | The procedure number from approval no longer exists. | Same as “chart changed.” Fetch, approve again. |
| Editing a received ClaimProc can delete income transfers | Open Dental’s own warning: changing a received line has side effects. | If you see unexpected transfers disappear in the chart, stop and call Ordo / your OD admin. |

Ordo tries to be careful: if a line is **already** attached to a check, it does **not** send a Status change; it still may send `InsPayAmt`. If Open Dental still refuses, you will see the “attached to a check” style 400.

### Posting — mark claim received (`PUT /claims/…`)

| You might see (idea) | Meaning | What to do |
| --- | --- | --- |
| Claim not found (404) | The claim was deleted or the number is wrong. | Fetch; if the claim is gone, it must be re-created in Open Dental. |
| 400 with explanation | Open Dental rejected the status/date update (invalid status letter, date format, or a locked claim). | Copy the explanation. Check the claim in Open Dental (already Received? locked?). Contact Ordo if the money posted on lines but the claim header did not. |

After a successful post, the claim should show as **Received** (**R**) with a date received.

### Posting — create the check (`POST /claimpayments`)

| You might see (idea) | Meaning | What to do |
| --- | --- | --- |
| **ClaimPaymentBatchOnly** is true / cannot use this method | The office preference requires **batch** insurance payments only. The single-claim finalize API is turned off. | Post that check in Open Dental with the office’s usual batch payment screen, or ask an OD admin about the preference. Contact Ordo so we know this clinic needs a different posting path. |
| **CheckAmt** must match the total of ClaimProcs’ InsPayAmt … ClaimPaymentNum of 0 | The check amount Ordo sent does not equal the unpaid received lines on the claim. | Often means some lines were already attached to another check, or amounts changed. **Look at the chart.** Do not post twice. Fetch and review. |
| Claim not found (404) | Claim number missing or deleted. | Same as above. |
| 201 with **ClaimPaymentNum** | Success — this is the number in the Ordo toast. | You are done. |

### Reject remark (`PUT` note on a claimproc)

Reject still succeeds in Ordo even if this note write fails. You may see a failed API log with a 400/404 while the toast says the match was rejected. The money was **not** posted.

---

## Messages Ordo adds (not raw Open Dental)

These are Ordo’s own sentences. They still usually mean “something about Open Dental.”

| You see | Meaning | What to do | Need Ordo? |
| --- | --- | --- | --- |
| **Open Dental is not connected. Save API keys in Settings → Integrations.** | No customer key (and/or developer key) on file. | Admin: paste customer key, Test, Save, Sync. | Yes if Test still fails with a current key. |
| **The Ordo developer key is not configured…** | Platform key missing. | Ordo staff (Administrator). | **Yes** |
| **Add the clinic customer key in Clinic settings → Integrations.** | Practice key missing. | Paste the key from Open Dental support. | No, unless you do not have a key. |
| **Open Dental changed since approval** | After approve, a line disappeared, a **code** changed, or a line already has a different `InsPayAmt`. | Fetch, read lines, approve, post **once**. | Yes if it repeats with nobody editing the chart. |
| **ClaimProc {number} is no longer on the Open Dental claim** | That procedure was removed or moved after you approved. | Fetch and pick the claim again. | No if you can see the change in OD. |
| **ClaimProc {number} code changed (D1110 → D0120)** | Someone changed the code sent on that line. | Fetch, confirm you still want this visit. | No |
| **ClaimProc {number} already has InsPayAmt $80, expected $100** | Money is already on the line, and it is not the amount Ordo planned. | Open Open Dental. If it is the same payment, stop. If it is old estimate leftover vs EOB, decide with your office policy; often you must receive it in OD by hand. | **Yes** if you are unsure whether it is this remittance. |
| **Verify failed for ClaimProc {number}: expected InsPayAmt …** | Ordo wrote (or thought it wrote), then re-read the line and the amount did not match. | **Check Open Dental.** Partial write is possible. Do not post again until you know. | **Yes immediately** |
| **Cannot post payment: Open Dental ClaimNum is missing on this match.** | The approved snapshot has no claim number. | Reject, fetch, approve again. | Yes if it happens on a clearly matched claim. |
| **Push package has no ClaimProc lines** | Approve produced an empty write list (no matched procedures). | Do not post. Pick a claim with matching codes, or post by hand. | No |
| **Push package not found** / **approved push package are required** | Post ran without a fresh approve. | Approve again, then post. | No |
| **Connection test failed** | Test’s GET claims call failed. The toast/API Logs have the Open Dental body. | Use the HTTP table above. | Yes if Test fails with a saved, current key. |
| **Open Dental sync failed** / **Open Dental fetch failed** | Read path failed. | Test, then retry Sync/Fetch once. | Yes if it lasts. |
| **Failed to load Open Dental status** | Integrations screen could not load last sync. | Refresh. Sign in again. | Yes if it persists. |

---

## After a post failure — decision tree

```
Post payment failed
        │
        ▼
Open the claim in Open Dental.
        │
        ├── Insurance payment / check is already there
        │         → STOP. Contact Ordo. Do not post again.
        │
        ├── Claim looks unchanged (still not received, $0 paid)
        │         → Read the toast.
        │         → If “changed since approval”: Fetch, approve, post once.
        │         → If 401/eConnector: Test, then post once.
        │         → If 429/504: wait, then post once.
        │
        └── You cannot tell
                  → STOP. Contact Ordo with EOB ID, time, and API Logs error text.
```

---

## What to send Ordo (copy and fill in)

Do **not** paste the customer key, the full EOB PDF, or screenshots of patient names.

```
What I was doing (Test / Fetch / Sync / Post):
Exact message (from toast or API Logs):
HTTP status (if shown, e.g. 400):
Endpoint if shown (e.g. PUT /claimprocs/293):
EOB ID:
Time and timezone:
Demo or Actual:
Did I already click Post payment? (yes/no)
Does Open Dental already show the insurance payment? (yes / no / not sure)
```

If posting might have happened twice, say that in the first sentence.

---

## Related pages

- [What each operation does](../workflows/operations.md)
- [Statuses](../workflows/statuses.md)
- [Errors and getting help](index.md)
- [Clinic settings](../modules/clinic-settings.md)
- [When something looks wrong](../examples/when-things-go-wrong.md)
