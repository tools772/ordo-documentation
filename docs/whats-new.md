# What's new

New modules and bigger changes in Ordo, newest first. Each entry links to the full guide.

---

## Release 2026.10.13 — EOB reading and posting fixes

*Released October 13, 2026.*

This release fixes the EOB problems practices reported in early October. It also makes the [Appointments, online booking, and patient messages](#october-2026-appointments-and-online-booking) modules available. Ordo turns those on per clinic.

!!! note "EOBs already in Ordo"
    Ordo does not re-read an EOB by itself. To apply the reading fixes below to an EOB you uploaded earlier, open it and click **Reprocess**. You can reprocess an EOB until one of its claims is approved or posted.

### Reading EOBs

- **Ameritas** EOBs now have their own layout. Before, services Ameritas paid could show as paid $0.
- **MetLife**
    - Claims whose table reads **Service code, tooth #, description** are no longer skipped.
    - A claim that runs onto the next page is now read as one claim, not two.
    - A note such as *$50.00 applied to deductible* is read as the deductible, not as the paid amount.
- **Delta Dental check disbursement** statements (for example Delta Dental of Illinois)
    - Lines with an area of the mouth (such as **LL**) or more than one message code are no longer dropped.
    - Each claim's paid amount now comes from the **TOTAL** line Delta prints. If Ordo ever misses a line, the claim shows a mismatch instead of a smaller total.
- **Delta Dental portal printouts** repeat the last lines of a page at the top of the next one. Ordo no longer reads those lines twice, so real procedures are no longer marked as duplicates.
- **Delta Dental of Washington** payment vouchers are now supported, including the check date.
- **Cigna** claims that continue across pages no longer show the same lines on two claims.
- **Deductibles** on MetLife and Delta check disbursement EOBs are no longer added on top of the patient amount, which already includes them.
- For layouts read with AI: if every line comes back as paid $0 but the claim paid more, Ordo now fills in each line's paid amount.

Read: [What files and layouts Ordo reads](workflows/supported-formats.md)

### Patients

- **Brothers and sisters on one policy stay separate patients.** Before, when family members shared the subscriber's member ID, every claim was saved under whoever was added first. Records already in Ordo have been corrected.
- A new **Family** tab on each patient's page lists everyone on the same policy.

Read: [Patients](modules/patients.md)

### Posting to Open Dental

- **One visit paid as several claims.** Payers sometimes pay part of a visit, such as a sealant, on its own claim number, while Open Dental has one claim. Ordo now matches, approves, and posts those claims together as that one Open Dental claim. Before, posting one part could mark the other part's lines as received $0.
- **No more date errors from a missing check date.** If the EOB has no check date, the EOB page says so and lets you enter it. If you don't, Ordo sends the claim's processed date (or today) instead of a blank date.
- **Already posted claims** are recognised from Open Dental's own message and shown as **Already Posted**, not **Failed**.
- **No duplicate checks.** Ordo never retries creating a claim payment by itself, so a slow connection cannot create a second check in Open Dental.

Read: [Post a payment](workflows/posting-a-payment.md) · [Open Dental errors](errors/open-dental.md)

### Correcting an EOB before you post

- Use the pencil next to **Check date** on the EOB page to fix the **check date and check number**.
- Use **Edit patient & claim** on a row to fix who the claim belongs to and its claim details.
- If you edit a procedure's insurance-paid amount, that edited amount is what Ordo posts.
- Changing a claim or its procedures clears its approval, so you approve the amounts that will actually be posted.
- Edits lock once a claim is posted, and every edit is recorded in the audit trail.

Read: [Inside an EOB](modules/working-an-eob.md)

### Underpayment checks

- **Patients with two insurances.** A procedure is now judged on what the primary and secondary paid together. Lines from a secondary claim are marked **COB review** instead of being flagged as underpaid.

Read: [Check for underpayments on an EOB](workflows/payment-analysis.md)

### Online booking

- Patients can add a note under **Anything we should know?** when they book or reschedule. It is saved on the Open Dental appointment.
- Existing patients see the insurance you have on file when they book.
- Clinics choose which **visit types** patients can book.
- Staff are asked to confirm before rescheduling or cancelling a visit.

Read: [Online booking page](modules/online-booking.md) · [Set up online booking](workflows/set-up-online-booking.md)

---

## October 2026 — Appointments and online booking

Ordo now covers the front desk as well as insurance posting. These modules are turned on per clinic by Ordo. If you want them, email **[help@perfect.ventures](mailto:help@perfect.ventures)**.

### Appointments

Your Open Dental schedule inside Ordo.

- **Day, Week, and List** views, with filters for provider, status, insurance, and how the visit was booked.
- **List view** with sorting and pages of 25, 50, or 100.
- **Book appointment** for patients on the phone, including new patients, straight into Open Dental.
- **Reschedule** into open times and **Cancel** (marked Broken and moved to the Unscheduled List, no fee posted).
- Appointment **colours**, team **comments**, and **files** on each visit.
- A read-only **Patient** tab with contact details, alerts, and balance.
- **Export .ics** to put the schedule you are looking at into Google Calendar, Apple Calendar, or Outlook.
- Markers for visits **booked online** and **booked on call** through Ordo.

Read: [Appointments](modules/appointments.md) · [Book an appointment on a call](workflows/book-by-phone.md)

### Online booking page

A web page where patients book their own visit from your real Open Dental availability, and reschedule or cancel if you allow it.

- New and existing patients, with matching against Open Dental so existing patients are not duplicated.
- Optional insurance details and card upload, saved to the appointment note for your team to verify.
- An **insurance list** you control (accepted, not accepted, most common first).
- A **website button** you can paste into your site.

Read: [Online booking page](modules/online-booking.md) · [Set up online booking](workflows/set-up-online-booking.md)

### Patient messages

Emails and texts to patients who book online: confirmation, reminders 24 hours and 2 hours before, forms reminder, and notices when they reschedule or cancel online. Your wording or Ordo's, with a **Testing mode** that sends everything to your own contacts first.

Read: [Patient messages](modules/patient-messages.md)

### Clinic settings

- New **Modules** tab — which modules Ordo has turned on for your clinic (EOB processing, Analytics and its screens, Appointments). Read only.
- New **Appointments** tab — the booking page, website button, testing mode, patient messages, and insurance list.
- Three new role permissions under **Appointments**: **View schedule**, **Edit details**, **Reschedule and cancel**.

Read: [Clinic settings](modules/clinic-settings.md) · [Roles and who can do what](people/roles.md)

Errors for all of the above: [Appointments and booking errors](errors/appointments.md).

---

## Earlier

- **Analytics** grew into four pages — Posting Analytics, Payment Analytics, Fee Analysis, and Analytics AI — and the old **Reports** page became Posting Analytics → Overview. See [Analytics](modules/analytics.md).
- **Fee schedules and date maps** per insurer, for underpayment checks. See [Set up fee schedules and date maps](workflows/fee-schedules.md).
