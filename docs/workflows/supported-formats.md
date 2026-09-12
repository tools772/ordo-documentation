# What files and layouts Ordo reads

You do **not** pick an insurance company when you upload. Drop the remittance; Ordo detects the printed layout and pulls out patients, claims, and procedure amounts.

This page is the catalog of what that reader understands **today**. Layouts not listed here land in **Failed**. Post those checks in Open Dental by hand, then [archive the file](../modules/eob-dashboard.md) so it does not sit in Failed forever.

---

## Files you can drop

On **EOB Dashboard → Upload EOBs**:

| Kind | What to use | How Ordo reads it |
| --- | --- | --- |
| **PDF** | A remittance export from the payer portal (best) | Selectable text is read directly. |
| **PDF scan** | A PDF with no selectable text (a scanned printout) | Ordo runs on-server OCR, then the same layout reader. |
| **JPG / JPEG / PNG** | A photo or screenshot of the remittance | Same on-server OCR path. No extra OCR product to turn on. |

Each file can be up to **50 MB**.

!!! tip "Prefer a portal PDF"
    A text PDF from the payer portal is still the most reliable. Photos work when the page is flat, well lit, and fully in frame. Blurry, cropped, or dark pictures often fail even when the layout is supported.

**Not for upload:** Word files, Excel, password-protected PDFs, claim *forms* (the paper you sent *to* insurance), eligibility letters, and patient-facing “this is not a bill” statements that are not the remittance.

The upload dialog also has **What’s supported?** — the same list, in short.

---

## Layouts Ordo detects automatically

A **layout** is the printed template, not just the company name. Delta Dental, for example, prints several different forms; Ordo has a reader for each one below, not a single “Delta” switch.

### Cigna

| Layout | What it looks like on the page |
| --- | --- |
| **Cigna Dental** | PPO remittance — “Explanation of dental payment,” patient blocks with procedure lines. |
| **Cigna DHMO** | Cigna Dental Health **supplemental and office-visit payments closing report** (not the PPO form). |

### MetLife and Guardian

| Layout | What it looks like on the page |
| --- | --- |
| **MetLife** | **Patient Benefits Statement** with payment, then a claim-detail block per patient. |
| **Guardian** | **Provider Explanation of Benefits** (often delivered through ECHO), with ADA code columns. |

### Blue Cross Blue Shield

| Layout | What it looks like on the page |
| --- | --- |
| **BCBS (HCSC)** | Blue Cross Blue Shield of Illinois or Texas (Health Care Service Corporation) claim detail / claim lines. |

### Delta Dental (several printed forms)

Delta is not one template. If the footer or title matches one of these, it should extract. Other Delta printouts (a different state form, a letter, a portal screenshot that is not a remittance) may still fail.

| Layout | Typical plans / title |
| --- | --- |
| **Delta EOB_DDS** | Shared **EOB_DDS** form (Ohio, Michigan, and other member companies that print that same footer). |
| **Delta Dental of Missouri** | Missouri explanation of benefits. |
| **Delta Dental of Oklahoma** | Oklahoma claim payment statement. |
| **Delta Explanation of Payment** | Northwest-style **Explanation of Payment** (Alaska, Oregon, and similar). |
| **Northeast Delta Dental** | Northeast Delta **Explanation of Benefits**. |
| **Delta Dental of Iowa** | Iowa portal **claim submission / claim details** printout. |

### Other carriers

| Layout | What it looks like on the page |
| --- | --- |
| **MCNA Dental** | MCNA claim detail with a **Services provided** block. |
| **United Concordia / Equitable** | United Concordia **QuicRemit** (also when Equitable is administered on that form). |
| **Envolve Dental** | Envolve **service(s) detail**. |
| **Physicians Mutual** | Physicians Mutual **Explanation of Payment**. |
| **Sun Life** | Sun Life dental **claim / procedure information**. |
| **DentaQuest** | DentaQuest or **TX HHSC Dental Program** claim detail. |
| **Careington** | Careington / **Maximum Care Network** explanation of payment. |

---

## What happens after you drop a file

1. The file is stored.
2. Status moves **Uploaded → Queued → Extracting**.
3. Ordo detects a layout from the list above (no carrier picker).
4. Status becomes **Extracted** — or **Failed** with a reason.

You still **Fetch Open Dental** and **Approve match** before anyone posts. Reading the file never writes to the chart.

Clinic **Insurance** settings (aliases, sample files, which catalog formats this office uses) do **not** change what the reader can parse. Upload stays format-agnostic. See [Clinic settings](../modules/clinic-settings.md).

---

## When reading fails

| You see | Usual meaning | What to do |
| --- | --- | --- |
| **We don't read this layout yet** / **Unsupported EOB format** | The page is not one of the templates above. | Confirm it is the remittance, not a letter. If it *is* a listed layout, email **[help@perfect.ventures](mailto:help@perfect.ventures)** with the EOB ID. Otherwise post in Open Dental by hand and archive the file. |
| **OCR ran but found little readable text** | A photo or scan was too poor to read. | Take a sharper, full-page picture, or re-export a text PDF from the portal. |
| **No extractable text** / older **OCR is not supported** | Empty PDF text, and OCR could not recover it (or an older failed job still shows the old wording). | Upload a JPG/PNG or a portal PDF. |
| **Recognised this as … but found no claims** | The header matched but no procedure lines were found. | Re-export a clean remittance. Contact Ordo if a normal listed file comes out empty. |

Full decoder: [Errors and getting help](../errors/index.md). Stories: [When something looks wrong](../examples/when-things-go-wrong.md).

---

## Related pages

- [EOB Dashboard](../modules/eob-dashboard.md) — where you upload
- [Post a payment](posting-a-payment.md) — after the file is Extracted
- [Clinic settings](../modules/clinic-settings.md) — Insurance tab (catalog, aliases, sample files)
