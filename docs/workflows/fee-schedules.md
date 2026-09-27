# Fee schedules and date maps

Ordo can only tell you whether an insurer underpaid if it knows **what they agreed to pay**. That is what fee schedules are for.

- A **fee schedule** is a list of CDT codes and fees — “Cigna PPO 2026: D1110 $104, D2750 $865, …”.
- A **date map** says **when** a fee schedule applies — “Cigna PPO 2026 applies from 2026-01-01 onward.”

Payment Analysis, Payment Analytics, and Fee Analysis all look up fees the same way: **insurer + CDT code + date of service**.

You manage both in **Clinic settings → Insurance**. Changing them needs the **Manage fee schedules** permission (Owners and Admins by default).

---

## Where they live

Clinic settings → **Insurance** has two sub-tabs:

| Sub-tab | What is in it |
| --- | --- |
| **Insurers** | One row per insurance company. Open an insurer to see its **Formats** (which EOB layouts it sends) and its **Fee schedule** (contracted fees and date maps). |
| **Office Fee / UCR (N)** | Your office’s own fees (UCR / usual and customary). N is how many Office / UCR schedules you have. |

Office / UCR fees are shown next to contracted fees for comparison. They are **never** used to calculate an underpayment.

---

## Add a fee schedule

Open an insurer’s **Fee schedule** tab (or **Office Fee / UCR**), then click **Add fee schedule**.

1. **Name** — something you will recognize next year, such as `Cigna PPO 2026`.
2. **Insurance provider (optional)** — already filled in when you start from an insurer. On the Office tab it says **None — office / UCR**.
3. **Get fees from** — pick one:
    - **Upload file** — a `.txt`, `.tsv`, or `.csv` with columns **CDT, fee, abbreviation, description** (tab- or comma-separated). Up to 5,000 codes. **Download sample** gives you a template.
    - **Open Dental** — choose one of your Open Dental fee schedules from the list (**Refresh list** if it is empty), then click **Fetch fees**. This uses the Open Dental connection for the location you are in.
4. Check the code count (for example “412 codes ready to save”), then **Save fee schedule**.

Saving a schedule does **not** make it apply to any dates yet. You still need a date map.

---

## Add a date map

At the top of the insurer’s Fee schedule tab (or the Office Fee / UCR tab), the **Date mapping** card lists which schedule applies for each date range.

1. Click **Add date map**.
2. In **Add date mapping**, choose the **Fee schedule**.
3. **Effective from** — the first date of service it covers.
4. **Effective to (optional)** — leave empty for “until further notice.”
5. **Label (optional)** — for example `Cigna PPO CY2026`.
6. **Save mapping**.

To stop using a mapping, click **Remove** on its row. The fee schedule itself stays.

**Overlaps are blocked.** For one insurer, two date ranges cannot cover the same day. If you try, you see *Date range overlaps an existing mapping (…)*. Close the old range first — give it an **Effective to** date — then add the new one.

All Office / UCR maps share **one** timeline in the same way.

---

## How Ordo picks the fee for a date of service

For each procedure, Ordo:

1. Finds the insurer’s date maps that cover the date of service.
2. Uses the one with the **latest Effective from** date.
3. If the insurer has no covering map, tries its **parent carrier** (for example a regional plan that shares the national schedule). Fee Analysis marks this with a **parent** badge.
4. Looks up the CDT code in that schedule.

If nothing is found, the line shows **NA** with **Missing clinic fee** / **Fee schedule review**, and no underpayment is claimed.

---

## Example: Bright Smile’s 2026 Cigna contract

Cigna sends Bright Smile a new fee schedule starting January 1, 2026.

1. Sarah opens **Clinic settings → Insurance → Insurers → Cigna → Fee schedule**.
2. **Add fee schedule**: Name `Cigna PPO 2026`, **Upload file**, picks the spreadsheet Cigna sent (saved as CSV). 388 codes. **Save fee schedule**.
3. In **Date mapping**, the existing row says `Cigna PPO 2025 · 2025-01-01 → open`. She removes it and re-adds it as 2025-01-01 → 2025-12-31.
4. **Add date map**: `Cigna PPO 2026`, Effective from 2026-01-01, Effective to empty. **Save mapping**.
5. She checks with [Fee Analysis](../modules/fee-analysis.md) on 2025-12-31 and 2026-01-02 that the fees change.

Claims from 2025 still use the 2025 fees. Claims from 2026 use the new ones.

### Office / UCR — one schedule for all dates

If your office fees rarely change, you do not need a map per year. Bright Smile keeps one Office / UCR map: **Office Fees**, 2022-01-01 → open. Every date of service since 2022 uses it.

---

## Common problems

| What you see | Likely cause | Fix |
| --- | --- | --- |
| Many lines show **NA** / **Missing clinic fee** | The insurer has no date map covering those dates, or the mapped schedule is missing those codes. | Add or extend the date map; add the missing codes to the schedule. |
| **—** in almost every row in Fee Analysis | The mapped schedule is empty or has only a handful of codes (for example a schedule fetched from a nearly empty Open Dental book). | Replace it with a complete schedule and re-map. |
| New fees did not take effect | The old map is still open-ended, or the new map starts on the wrong date. | Give the old map an **Effective to** date; check **Effective from** on the new one. |
| *Date range overlaps an existing mapping* | Two ranges for the same insurer cover the same day. | Close the older range first. |
| The schedule you want is not in the **Add date mapping** list | The list only shows schedules tagged to this insurer, or already mapped to it. | Add the schedule from this insurer’s Fee schedule tab (or pick this insurer as its provider). |

After fixing a schedule, run the analysis again — saved results keep the fees they were calculated with.

---

## Related pages

- [Clinic settings](../modules/clinic-settings.md)
- [Fee Analysis](../modules/fee-analysis.md)
- [Payment Analysis inside an EOB](payment-analysis.md)
- [Payment Analytics](../modules/payment-analytics.md)
