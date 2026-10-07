# Appointments and booking errors

Messages you may see in **Appointments**, on your **online booking page**, and in **Patient messages** — what they mean, what to try, and when to email **[help@perfect.ventures](mailto:help@perfect.ventures)**.

General advice for every error: [Errors and getting help](index.md). Open Dental error codes: [Open Dental errors](open-dental.md).

---

## Opening the Appointments page

| Message | Usually means | Try | Contact Ordo? |
| --- | --- | --- | --- |
| **Appointments isn't enabled for this clinic** | Ordo has not turned the module on for your practice. | — | **Yes**, to turn it on. |
| **Connect Open Dental to see appointments** | This location has no working Open Dental connection. | Owner or Admin: **Clinic settings → PMS Integrations** → Test. | If Test fails. |
| **We couldn't load the schedule** | Open Dental did not answer in time, or the connection dropped. | **Try again**, then **Refresh schedule**. | If it keeps happening. |
| **We couldn't load the Appointments module** | Ordo could not read your clinic's module settings. | Reload the page. | If it keeps happening. |
| **Choose a range of 31 days or less.** | The schedule can show at most a month at a time. | Use Day, Week, or List. | No. |
| **{N} patient names could not be loaded from Open Dental…** | Some names timed out; those rows show **Patient #1234**. | **Refresh schedule**. | No. |
| **Open Dental is busy. Try again shortly.** | Open Dental is rate-limiting requests. | Wait a minute and refresh. | If it lasts more than an hour. |
| **Open Dental rejected the request** | The customer key was rejected or does not allow this. | Owner or Admin: re-test the connection. | If the key is correct. |

## Reschedule, cancel, and book

| Message | Usually means | Try | Contact Ordo? |
| --- | --- | --- | --- |
| **That time is no longer open. Pick another time.** | Someone booked that time a moment ago. | Pick another time. | No. |
| **No open times for this provider on {day}. Try another day or provider.** | Open Dental shows no openings for that provider that day. | Another day or provider; check the provider's schedule in Open Dental. | No. |
| **Only scheduled appointments can be rescheduled.** / **…cancelled.** | The visit is already complete or broken. | Change it in Open Dental if needed. | No. |
| **Rescheduling isn't enabled for this clinic.** / **Cancelling isn't enabled…** | Your clinic does not allow it (set by Ordo). | Do it in Open Dental. | **Yes**, if your clinic should allow it. |
| **You do not have permission to do that** | Your role lacks **Reschedule and cancel** or **Edit details**. | Ask an Owner or Admin. | No. |
| **A patient with this name and date of birth is already in Open Dental…** | The “new” patient already has a chart. | Book under **Existing patient**. | No. |
| **The patient was added to Open Dental, but the appointment could not be booked…** | The chart was created; the visit was not. | Search under **Existing patient** and book again. Do not re-add them. | If it fails again. |
| **Appointment not found in Open Dental.** | The visit was deleted in Open Dental. | **Refresh schedule**. | No. |
| **You need access to Patients to see patient details.** | Your role lacks **View patients**. | Ask an Owner or Admin. | No. |

## Colour, comments, and files

| Message | Usually means | Try |
| --- | --- | --- |
| **Open Dental didn't save the colour. Try again.** | Open Dental accepted the request but did not keep the colour. | Try again; if it persists, set it in Open Dental. |
| **Comment saved in Ordo, but Open Dental didn't accept the note.** | The comment is in Ordo; copying it into the note failed. | Add it to the note in Open Dental if it matters there. |
| **You can only remove your own comments.** | Someone else wrote it. | Ask them, or an Owner. |
| **{file} is larger than 10 MB.** | Files are limited to 10 MB each. | Compress or split the file. |
| **{file} isn't an allowed file type…** / **…doesn't match its extension** | Not an accepted type, or the file was renamed. | Save it as PDF or an image. |
| **Attach up to 10 files at a time.** | Too many at once. | Attach in batches. |
| **File storage isn't set up for Ordo yet.** | File storage is not configured in this environment. | Email help@perfect.ventures. |

---

## What patients may see on the booking page

If a patient calls about one of these, this is what it means.

| Patient sees | Usually means | What the office can do |
| --- | --- | --- |
| **Online booking isn't available here** | The page is switched off, the web address changed, or the link is wrong. | Check **Accept online bookings** and the **Booking URL** in **Clinic settings → Appointments**. |
| **We couldn't load online booking** | A temporary problem. | Ask the patient to try again; book by phone meanwhile. |
| **We're having trouble checking appointment availability.** | Ordo could not reach Open Dental for this location. | Check **PMS Integrations**. Email Ordo if Test passes but patients still see this. |
| **Online booking isn't available for this visit type. Please call the office to schedule.** | No visit type is set up for this kind of patient (new or existing). | Email Ordo to add or change visit types. |
| **No appointments are available on these dates.** | No openings in Open Dental within your booking window. | Check provider schedules in Open Dental. |
| **That time was just booked. Please select another appointment.** | Someone else took the time. | Nothing — the patient picks another. |
| **Your session expired. Please confirm your details again to continue.** | The patient took more than about 45 minutes. | Nothing — they re-enter their details. |
| **We couldn't find your record…** | Name or birthday does not match Open Dental exactly. | Check spelling and birthday in Open Dental; or the patient continues as new (Ordo will flag a possible duplicate in the note). |
| **We couldn't find an upcoming appointment with those details…** (manage) | Name, birthday, or phone does not match, or there is no upcoming visit. | Check the phone numbers on the chart in Open Dental. |
| **Changes must be made at least {N} hours before your visit.** | Inside your clinic's patient change cutoff. | Staff can still change it in Ordo or Open Dental. |
| **This appointment is too soon to change online.** | Same as above, checked again at the last moment. | As above. |
| **This appointment was changed since you looked it up.** | Staff changed the visit while the patient was looking. | The patient looks it up again. |
| **Online changes are not available. Please call the office.** | Your clinic does not allow online rescheduling or cancelling. | Email Ordo if it should. |
| **Too many attempts. Please wait a few minutes and try again.** | Many tries from the same connection in a short time (a safety limit). | Wait about 10 minutes, or book by phone. |
| **Uploads aren't available right now. Please bring the files to your visit.** | File upload is temporarily unavailable. | Ask the patient to bring the card. |

---

## Patient messages

| Message | Usually means | Try |
| --- | --- | --- |
| **Add your forms link first.** / **Add your forms link before turning on the forms reminder.** | The forms reminder needs a link. | Save a **Forms link** starting with `https://`. |
| **Add a test email or phone before turning on testing mode.** | Testing mode needs somewhere to send. | Save a test contact first. |
| **Save a test email/phone under Testing mode first.** | **Send test** has nowhere to send. | Save a test contact. |
| **Set up your booking page first, then send a test.** | No booking page exists for this location yet. | Create the page under **Online booking page**. |
| **Too many test messages. Wait a few minutes and try again.** | More than 10 tests in 10 minutes. | Wait. |
| **{{x}} isn't a variable Ordo knows.** | A placeholder is misspelled. | Use the insert buttons instead of typing. |
| Status **Skipped** — *Email isn't set up yet* / *Text messages aren't set up yet* | The channel is not connected for your clinic. Skipped messages are not sent later. | Email help@perfect.ventures. |
| Status **Failed** | The provider refused it (bad address, number not a mobile). | Check the patient's contact details in Open Dental. |

---

## When you email Ordo

Include the location, the page (Appointments, booking page, or Patient messages), the exact message, and roughly when it happened. For a booking problem, include the booking page address. **Do not** include patient birthdays, member IDs, or screenshots of charts.

---

## Related pages

- [Appointments](../modules/appointments.md)
- [Online booking page](../modules/online-booking.md)
- [Patient messages](../modules/patient-messages.md)
- [Errors and getting help](index.md)
- [Open Dental errors](open-dental.md)
