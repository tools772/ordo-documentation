---
search:
  exclude: true
---

# Step 1 — Reading the EOB

**The question:** what does this remittance say — who was paid for, for which procedures, how much, on which check?

Reading never touches Open Dental. Nothing is written to a chart until someone approves and posts (steps 3–4).

---

## What Ordo does

### 1. Store the file and recognise the layout

You upload a PDF, a scanned PDF, or a photo (JPG/PNG, up to 50 MB). Ordo then works out the **printed layout** — not just the insurance company. Delta Dental alone prints more than a dozen different forms, and each has its own reader.

- **Text PDF** (exported from a payer portal): Ordo reads the text and its position on the page.
- **Scan or photo**: Ordo runs OCR (text recognition) on every page first, then uses the same readers. If the OCR quality score is low, it retries with up to three clean-up passes (grayscale, enlarge, straighten).
- The first reader whose fingerprint matches wins. Fingerprints are things like a title ("Explanation of dental payment"), a footer ("EOB_DDS"), or a column header.

With **Detect & upload**, the file stops at **Confirm layout** so a person can check the guess before anything is extracted. The full list of layouts is on [What files and layouts Ordo reads](../workflows/supported-formats.md).

### 2. Pull out the check, patients, claims and lines

For every remittance Ordo extracts:

| Level | Fields |
| --- | --- |
| **Check** | Payer, check or EFT number, payment date, total amount |
| **Patient** | Name, subscriber / member ID, relationship, date of birth when printed |
| **Claim** | Claim number, date of service, provider, billed and paid totals |
| **Procedure line** | CDT code, tooth or quadrant, date of service, billed, allowed / contracted, deductible, coinsurance, **insurance paid**, patient share, remark codes |

A few rules apply to every reader:

- **CDT codes** must look like a letter plus four digits. Codes printed as `140` or `00150` get their leading `D` back (`D0140`, `D0150`).
- **Tooth vs quadrant.** `UL`, `UR`, `LL`, `LR` are quadrants. Delta's area codes `10 / 20 / 30 / 40` on quadrant procedures are quadrants, not teeth 10–40. Leading zeros are removed from tooth numbers.
- **Dates are calendar days.** Ordo never converts them through a clock time, because that moved an Aug 18 visit to Aug 17 for one clinic. Two-digit years below 70 are read as 20xx.
- **Patient share** on a line = deductible + coinsurance when those are printed; otherwise billed − insurance paid.

### 3. Decide who each patient is

Several patients can share one subscriber ID (a parent's policy covering children). Ordo identifies a patient by **subscriber ID plus first and last name**:

- Small differences in the same person's name still match: middle initials, upper vs lower case, "Last, First" order, a stray extra word.
- **Jr / Sr / II / III / IV must match exactly**, so a father and son on the same policy stay two people.
- A one-word name only matches the identical one-word name.
- A claim printed with no name at all goes to the first patient already seen on that subscriber ID.

### 4. Check the totals

Ordo adds up the numbers it read:

- Each claim's line payments should equal the claim's paid total.
- All claims should add up to the check amount.
- The tolerance is **2 cents**.

If the totals do not add up, Ordo lowers its confidence in the read and records which claim was off.

### 5. When no reader fits

Each clinic chooses how strict reading is:

| Setting | What happens |
| --- | --- |
| **Parser** | Only the built-in layout readers. Unknown layout → **Failed**. |
| **AI** | Every file is read by an AI model instead of a layout reader. |
| **Fallback** | Layout reader first. AI only if the layout is unknown **or** the reader found zero claims. |

The AI is told never to invent or calculate an amount and to leave a field blank rather than guess. Ordo then checks the AI's answer: at least one claim, every claim has lines, no negative or impossible amounts, codes that look like CDT codes. Anything that fails is rejected, not saved.

One exception to "never calculate": if the AI read **every** line as $0 paid but the claim shows money paid, Ordo copies the allowed (or contracted) column into the paid column — **only** if that column adds up to the claim's paid amount to the cent. Otherwise it leaves the lines alone.

### 6. Save

Everything is saved in one step: the check, the patients, the claims and the lines. If saving fails halfway, nothing is kept. The EOB moves to **Extracted** and waits for a person. Ordo never starts matching or posting on its own.

---

## Real cases

!!! example "Cigna — a claim continued onto the next page"
    **What happened.** A Cigna PPO claim for Maria ran onto page 2. Page 2 had four identical X-ray image lines and the same sealant on several teeth. Ordo treated the repeats as duplicates and dropped them, so the lines no longer added up to the claim. A tooth number printed right after `Tooth#/Quad/Arch:` was also being glued onto the charge amount.

    **What Ordo does now.** Lines on a continued page are matched to the claim by document number, claim number and patient, then **always added — never de-duplicated**, because identical rows on a remittance are real repeats. The tooth/quadrant field is split from the amount.

!!! example "UnitedHealthcare Dual Complete — several patients on one remittance"
    **What happened.** A remittance covering three patients put every procedure on the first patient's claim. Denied rows (ending in an exception code such as 1051) silently disappeared.

    **What Ordo does now.** Rows are grouped by **Encounter #**, and continuation pages with the same encounter are merged. Denied rows are kept, with their exception notes. Deductible, coinsurance and patient pay are carried onto each claim.

!!! example "UnitedHealthcare — capital letters and full-mouth ranges"
    **What happened.** Names printed in ALL CAPS were not found. The check number sat in a `UHC01U` footer when Ordo only knew `UHC01R`. A tooth range printed `01 32` was saved as tooth 1.

    **What Ordo does now.** Names are matched in any case. Any `UHC01` + letter batch ID is accepted as the check number. Two tooth numbers together are treated as a full-mouth range, so no single tooth is set.

!!! example "Ameritas — paid amount only on the TOTAL row"
    **What happened.** Ameritas prints **PAYABLE** only on the total row for each benefit group. Every line read as $0 paid while the claim showed $412 paid.

    **What Ordo does now.** A dedicated Ameritas reader spreads the group's deductible across its lines and pays each line (covered − deductible) × coverage %. Any rounding cent goes on the last line. Notes like "paid as D0120" (the payer paid a different code) are kept.

!!! example "Delta Dental of Washington — a check header with no labels"
    **What happened.** The insurer's name appears only in the logo. The check date and number are printed on the payee line with no labels: payee, tax ID, date, number. The patient details sit in a stack on the left.

    **What Ordo does now.** A dedicated voucher reader takes the unlabeled date and number from that line. The AI instructions carry the same rule, and say never to use a service, received, processed or birth date as the payment date.

!!! example "Sun Life — two layouts from one payer"
    **What happened.** Only Sun Life's online-portal printout was supported. Mailed Sun Life checks (with an EOB Number and Payment Cycle) failed.

    **What Ordo does now.** Each layout has its own reader, and tests confirm neither reader grabs the other's documents.

!!! example "Cigna — a deposit slip instead of the remittance"
    **What happened.** Jennifer uploaded Cigna's direct-deposit advice. It has payment totals but no patients or procedures, and she got a vague "AI validation failed" message.

    **What Ordo does now.** If the file looks like a deposit advice, payment summary or supplemental-payment summary and has no patient, procedure or date-of-service wording, Ordo says so and asks for the detailed remittance (or Cigna's supplemental closing report).

!!! example "United Concordia — remark A1"
    **What happened.** A line showed an allowed amount, but remark **A1** meant the whole allowance went to the patient's deductible.

    **What Ordo does now.** A line with remark A1 is read as **$0 paid**.

!!! example "Smaller layout quirks Ordo handles"
    - **Lincoln (QuicRemit):** the paid amount is printed glued to a reason code (`$62.00201`). Ordo separates them.
    - **Northeast Delta:** zero is printed as `$.00`, and labels are letter-spaced (`P AYMENT`).
    - **Delta EOB ODS (Kentucky):** "Originally submitted" and "Replaced by" lines are skipped so a replaced code is not paid twice.
    - **Delta Michigan:** a non-covered line where the patient owes the whole allowance reads correctly.
    - **Guardian:** the printed "Total benefit paid" is used rather than adding up the lines.
    - **Cigna DHMO:** member names wrapped onto two lines are joined back; separate visits for the same member stay separate claims.
    - **Equitable** printed on United Concordia's QuicRemit form is labelled Equitable.
    - **Delta portal scans:** OCR mistakes in codes (`O` for `0`, `I` or `L` for `1`) are corrected.

---

## What Ordo does not do yet

!!! warning "Known gaps — please tell us if you hit them"
    - **Some layouts read only one claim per check.** BCBS (HCSC), Delta Missouri, Oklahoma, Northwest Explanation of Payment, Northeast Delta, Iowa, Idaho, Kentucky (EOB ODS), New Jersey, Arkansas, MCNA, Envolve, DentaQuest, Careington, Mutual of Omaha, Aetna Medicare, ManhattanLife, Anthem / BCBS FEP, Principal, GEHA, Renaissance, Centene, UnitedHealthcare and the Delta portal printout. If one of these checks covers **more than one patient**, Ordo will merge them or miss some. Send us that file.
    - **Some readers were built from a single sample.** Premera, Centene, Renaissance, Careington, GEHA, UnitedHealthcare and the Delta portal (Georgia) printout. A second clinic's file from these payers may read wrong. Please send one.
    - **The "other insurance paid" column is not read.** Coordination-of-benefits amounts printed on the remittance are ignored when reading. (Payment analysis does handle dual insurance — see [Checking the money](checking-the-money.md).)
    - **A total that does not add up does not stop you.** It lowers Ordo's confidence but there is no banner yet. Cigna PPO files are not totals-checked at all.
    - **Some layouts put a claim's whole payment on one line** when the lines do not add up (Lincoln), or on a single summary line (Premera, Centene). The claim total is right; the split per procedure may not be.
    - **Uploading the same file twice** is not caught. You get two copies of every claim.

---

## Questions for your team

!!! question "Have you seen something different?"
    1. Do you receive checks from a payer **not** on the [layout list](../workflows/supported-formats.md)? Which ones, roughly how often?
    2. For the "one claim per check" payers above — do you ever get a single check covering several patients?
    3. Do any of your remittances print the paid amount **only** on a total row (like Ameritas)?
    4. Do you see lines that are legitimately repeated (same code, same tooth, same day)? From which payers?
    5. When a remittance includes a **denied** or **$0** line, do you want it to show in Ordo, or only paid lines?
    6. Do you ever get a **corrected** or **reissued** remittance for a check you already posted? How do you handle it today?
    7. Do photos or scanned paper EOBs make up a meaningful share of your volume?

---

[← The codebook](index.md) · [Next: 2. Finding the patient and claim →](finding-the-patient-and-claim.md)
