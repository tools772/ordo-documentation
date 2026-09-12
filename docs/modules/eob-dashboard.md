# EOB Dashboard

**EOB Dashboard** is the file inbox. Each row is one remittance PDF (or image), not one patient. Think of it as the stack of envelopes on the insurance desk: you drop new mail here, you open an envelope to work the people inside, and you archive envelopes you are done with.

Open it from the sidebar: **EOB Dashboard**.

---

## What you see at the top

Four summary cards (the exact numbers come from files your role can see):

| Card | Plain meaning |
| --- | --- |
| **Today’s uploads** | Files dropped in today. |
| **Pending review** | Files that still need a person. |
| **Payments posted** | Files that made it through to Open Dental. |
| **Failed jobs** | Files Ordo could not read, or posts that failed. |

There are also small charts (daily uploads vs posted, mix of statuses, payment value). They are a pulse check, not a financial close. For sliced numbers, use [Reports](reports.md).

---

## The file list

Each row typically shows:

- File name (for example `Cigna_EOB_2026-08-24.pdf`)
- An **EOB ID** (Ordo’s internal number — useful when you email support)
- When it was uploaded
- How far along it is (**Uploaded**, **Confirm layout**, **Queued**, **Extracting**, **Extracted**, **Failed**, **Archived**, …)
- When the layout is known but not processed yet: a **Confirm layout** badge and a subline like **Detected Cigna**
- Counts once reading finishes: patients, claims, procedure lines, payment amount

The row menu (three dots) includes **Download EOB** and, when the file is waiting for confirmation, **Process {payer}** (or **Process EOB**). **Download EOB** saves the original uploaded PDF or image to your computer — the file you dropped, not an Ordo export. Use it when you need to re-read the remittance, attach it to a support email (prefer EOB ID first), or compare it to what Ordo extracted.

### Search

Type part of the **file name** or **EOB ID**. This does not search patient names. For patient names, use the [Patients](patients.md) module.

**Example.** You remember the file was “the big Cigna from last Thursday” but not the patient. Search `Cigna`. Open the file. Then search for Maria inside that file.

### Status filters (tabs)

| Tab | What it includes |
| --- | --- |
| **Active** | Everything that is not archived. Your normal working list. |
| **Uploaded** | Arrived; may still need detect or confirm. |
| **Queued** | Waiting in line to be read. |
| **Extracting** | Ordo is reading the PDF right now. |
| **Extracted** | Reading succeeded; you can open and work it. |
| **Failed** | Reading (or a later step) failed. |
| **Archived** | Hidden from Active and from Reports. |

There is **no separate Confirm layout tab**. Files waiting for confirmation usually sit under **Active** or **Uploaded**, with the **Confirm layout** badge on the row.

### Uploaded date

Same date control as Reports. Presets include **today**, **last 7 days**, **last 30 days**, and **this month**. Combine it with a status tab.

**Example.** Friday afternoon, Jennifer wants only this week’s failed files:

1. Date preset: **last 7 days**
2. Tab: **Failed**
3. If the list is empty, nothing failed this week.

### Export

Export downloads the **current** list (after search and filters), not the entire history. Use it for a huddle spreadsheet or to attach to an email.

---

## Uploading EOBs

If your role includes **Upload EOBs**, you will see **Upload EOBs**. That opens **Upload EOB Documents**.

**Accepted files:** PDF, JPG, and PNG, up to 50 MB each. Prefer a **text PDF** from the payer portal. Photos and scanned PDFs are read with on-server OCR when needed.

### Three ways to upload

| Mode | What it does | Button |
| --- | --- | --- |
| **Upload** | Saves the file now. Detect and process later from the dashboard. | **Upload** |
| **Detect & upload** | Identifies the remittance layout, then asks you to confirm before extracting patients. | **Detect & upload** |
| **Fill from sample** | Download a sample, fill your text/CSV data, upload — it becomes the EOB. | **Upload template** |

**Detect & upload** is the usual Monday path:

1. Drop the remittance(s). Progress may say **Uploading & detecting…** / **Detecting…**.
2. Ordo shows what it found — for example “This looks like **Cigna** · 3 pages” with a **Ready** badge. Unrecognized files show **Unsupported**.
3. Toast: **Detected {payer} — confirm to process**.
4. Click **Process EOB** (or **Process EOBs** for several). Click **Later** if you want to confirm from the list or inside the file.

After you process, the row moves through Queued / Extracting and becomes **Extracted** — or **Failed** if reading fails.

You can also open a **Confirm layout** row and click **Confirm & process** on the file page, or use **Process {payer}** on the row ⋯ menu.

!!! note "Which insurance layouts work today?"
    Ordo auto-detects many remittance layouts, including **Cigna Dental**, **Cigna DHMO**, **MetLife**, **Guardian**, **BCBS (HCSC)**, several **Delta Dental** printed forms (not one Delta-for-all), **MCNA**, **United Concordia / Equitable**, **Envolve**, **Physicians Mutual**, **Sun Life**, **DentaQuest**, **Careington**, **Mutual of Omaha**, **Aetna Medicare**, **ManhattanLife**, **Lincoln Financial Group**, and **Premera Blue Cross**.

    The full table, file types, and OCR notes: [What files and layouts Ordo reads](../workflows/supported-formats.md).

    Other carrier layouts land as **Unsupported** or **Failed** with a clear message. That is a limitation of the reader, not a problem with your PDF viewer.

### Example: Jennifer uploads Monday’s remittance

1. Jennifer (Admin) opens **EOB Dashboard**.
2. She clicks **Upload EOBs**, chooses **Detect & upload**, and drops `Cigna_Remit_Aug24.pdf`.
3. Ordo shows **Ready · This looks like Cigna**. She clicks **Process EOB**.
4. When the status is **Extracted**, the row shows something like **3 patients, 3 claims, 8 procedures**.
5. She clicks the row to start work. (Mike could also open it; he cannot upload if his role forbids it.)

If she is in **Demo**, she may skip upload and use a sample file that is already there. Demo never writes to the live practice database.

---

## Opening a file

Click the row. You leave the inbox and enter [Inside an EOB](working-an-eob.md) — the patient list for that remittance. **Download EOB** is also on that page if you already have the file open.

Nothing has been posted yet. Opening is always safe.

---

## Archiving and restoring

If your role includes **Archive**:

- **Archive** takes the file out of Active and out of Reports. Use this for duplicates, test files, or remittances you will not post.
- **Restore** (from the Archived tab) puts it back.

Archiving is not deleting. The file and its extracted patients are still there.

**Example.** A coordinator uploaded the same PDF twice. Archive the duplicate so Reports does not double-count uploads. Work the copy that extracted cleanly.

---

## What your role changes on this screen

| Permission | What you can do here |
| --- | --- |
| EOB dashboard (view) | See the list and open files. |
| Upload EOBs | Drop new files. |
| Archive | Archive or restore files. |

Viewers can watch the inbox. They cannot upload or archive.

---

## Related pages

- [Inside an EOB](working-an-eob.md) — after you click a file
- [Patients](patients.md) — find a person without knowing the file
- [Reports](reports.md) — the same files, totaled
- [What files and layouts Ordo reads](../workflows/supported-formats.md)
- [Statuses](../workflows/statuses.md) — what Uploaded / Extracted / Failed mean
- [When something looks wrong](../examples/when-things-go-wrong.md)
