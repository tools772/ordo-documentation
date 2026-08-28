# Patients

**Patients** is a list of every person Ordo has read off every EOB — not grouped by file. Use it when you know the *person* but not which PDF they were on.

Open it from the sidebar: **Patients**.

This is not the Open Dental chart, and it is not a medical record. It is a **work queue of extracted names**.

---

## When to use Patients instead of the Dashboard

| You know… | Go to… |
| --- | --- |
| The file name, or “today’s Cigna remittance” | [EOB Dashboard](eob-dashboard.md) |
| “Maria Santos called — is her payment posted?” | **Patients** |
| You want totals for the week | [Reports](reports.md) |

**Example.** The front desk says Maria is at the window asking about her Cigna payment. Jennifer does not remember which remittance. She opens **Patients**, types `Santos`, sees the row, and clicks it. Ordo takes her to Maria *inside that EOB*, on the review screen.

---

## What each row shows

Typical columns:

- Name
- Patient ID / EOB patient id
- Subscriber
- Which EOB (file) she came from
- Open Dental id (once matched)
- Date of service
- Paid / plan covered amount
- Match status

Click a row to land on that patient inside the EOB (the same place as [Inside an EOB](working-an-eob.md)).

---

## Filters

| Filter | Meaning |
| --- | --- |
| **Active** | Everyone not archived. Default working list. |
| **Pending** | Matching has not finished or not started. |
| **Needs review** | A person should look (ambiguous or flagged). |
| **Matched** | A candidate was found. Still review before posting. |
| **No match** | Ordo could not find a plausible chart claim. |
| **Archived** | Hidden from Active. |

You can also search by name, identifiers, subscriber, or EOB.

**Example.** Mike wants a Monday punch list of only the hard cases: filter **Needs review**, sort by amount descending, work the largest dollars first.

---

## Archive a person (not the whole file)

If your role includes **Archive**, you can archive or restore a **patient row**.

That is different from archiving an entire EOB:

- Archive **file** — the whole remittance leaves the inbox and Reports.
- Archive **patient** — that person drops off the Patients active list (for example a duplicate extraction), without throwing away the rest of the file.

Use patient archive sparingly. If the whole check is a test upload, archive the **file** on the Dashboard instead.

---

## Export

Export uses the **current** filter and search. If you filtered to Needs review, the spreadsheet is only those people.

---

## What Patients will not do

- It will not let you chart treatment.
- It will not show patients who were never on an uploaded EOB.
- It will not post. Posting still happens on the Open Dental tab inside the file.

---

## Related pages

- [Inside an EOB](working-an-eob.md)
- [EOB Dashboard](eob-dashboard.md)
- [Roles and who can do what](../people/roles.md)
