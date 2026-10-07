# Patient messages

**Patient messages** are the emails and texts Ordo sends to patients who book on your [online booking page](online-booking.md): a confirmation, reminders before the visit, a nudge to fill in forms, and a notice when they reschedule or cancel online. Each one is signed with your clinic's name.

**Nothing is sent until you turn it on.** You choose which messages go out, by email, by text, or both, and you can use Ordo's wording or write your own.

Find it under **Clinic settings → Appointments**, in the **Testing mode** and **Patient messages** cards. Changing anything needs **Manage team and locations** (the screen calls it *the Manage clinic settings permission*).

---

## Who gets messages — and who does not

| Gets messages | Does not get messages |
| --- | --- |
| Patients who booked on your online booking page | Visits booked directly in Open Dental |
| Patients who reschedule or cancel from the booking page | Visits your team books in Ordo on a call |
| | Visits your team reschedules or cancels in Ordo |

Message settings apply to the **whole practice**, even if each location has its own booking page.

**Where messages go.** For existing patients, Ordo uses the email and phone in Open Dental (mobile first, then home, then work). For new patients, it uses what they typed on the booking page. Only US mobile numbers can receive texts.

**What patients see.** Emails come from Ordo's sending address with **your clinic's name** as the sender. If your booking page has a clinic email, replies go to it. Emails use a simple layout with your brand colour and end with *You're receiving this because you booked an appointment with {your clinic}.*

---

## The messages

| Message | Email | Text | When it goes out |
| --- | --- | --- | --- |
| **Appointment confirmation** | ✓ | ✓ | As soon as the patient books online. |
| **Appointment reminder — 24 hours before** | ✓ | ✓ | The day before. Skipped when the visit was booked less than a day ahead. |
| **Appointment reminder — 2 hours before** | | ✓ | Same day, within two hours of the visit. Not sent before 8 am or after 9 pm clinic time. |
| **Forms reminder — Send after booking** | ✓ | ✓ | Right after booking, with a link to your patient forms. Needs a **Forms link**. |
| **Cancellation — Cancelled online** | ✓ | ✓ | When the patient cancels from the booking page. |
| **Rescheduling — Rescheduled online** | ✓ | ✓ | When the patient picks a new time from the booking page. |
| **Booking started but not finished** | | ✓ | *Coming later* — shown but cannot be turned on yet. |

Each row has a switch per channel, and an **Edit** button to change the wording. An **Edited** badge appears once you have changed it from Ordo's wording.

### Forms link

The forms reminder needs a link to your online patient forms. Enter it in **Forms link** (it must start with `https://`) and click **Save link**. Until there is a link, the forms reminder cannot be turned on.

### When email or texts are not set up

The card shows a badge if a channel is not connected for your clinic yet:

| Badge | Meaning |
| --- | --- |
| **Email not set up** | Ordo has not connected email for this environment. |
| **Texts not set up yet** | Ordo has not connected text messaging for your clinic yet. |

You can still switch messages on. They are saved and logged as **Skipped** (*Email isn't set up yet* / *Text messages aren't set up yet*) — they are **not** sent later when the channel is connected. Email **[help@perfect.ventures](mailto:help@perfect.ventures)** to get a channel connected.

---

## Reminders: the timing rules

Ordo checks for reminders every 15 minutes.

- **Quiet hours.** No reminders between 9 pm and 8 am, clinic time.
- **24 hours before.** Sent the day before the visit, as early as 27 hours before. Only for visits booked at least 24 hours ahead.
- **2 hours before.** Sent on the day, within two hours of the visit. Only for visits booked at least 12 hours ahead. Because of quiet hours, very early visits (for example 7 am) get no 2-hour text.
- **Before each reminder**, Ordo checks Open Dental. If the visit was cancelled (in Ordo, in Open Dental, or by the patient), nothing is sent. If it moved, the reminder follows the new time.

**Each message goes out once.** A confirmation is sent once per booking; a reminder once per appointment time (so a moved visit gets fresh reminders); a reschedule notice once per new time; a cancellation once. A failed reminder is retried a couple of times on later checks. A failed confirmation is **not** retried. A failed message never cancels or blocks the booking.

---

## Editing a message

Click **Edit** on a message. The editor shows:

- **Subject** (email only, up to 200 characters).
- **Message** (up to 5,000 characters for email, 640 for text).
- *Insert a detail where your cursor is:* — buttons that drop in a placeholder.
- A **preview** using a sample patient (Alex Rivera, Dr. Smith, *Cleaning & exam*, tomorrow at 9:30 AM).

Buttons: **Use Ordo's wording** (go back to the default), **Send test to {your test contact}**, **Cancel**, and **Save message**.

### Details you can insert

| Button | Placeholder | Example |
| --- | --- | --- |
| Patient first name | `{{patient_first_name}}` | Maria (uses the preferred name if set; “there” if unknown) |
| Patient full name | `{{patient_full_name}}` | Maria Santos |
| Clinic name | `{{clinic_name}}` | Bright Smile Dental |
| Clinic phone | `{{clinic_phone}}` | (555) 555-0100 |
| Clinic email | `{{clinic_email}}` | frontdesk@brightsmile.com |
| Clinic address | `{{clinic_address}}` | 12 Main St, Springfield |
| Provider | `{{provider_name}}` | Dr. Priya Gupta |
| Visit type | `{{appointment_type}}` | Cleaning (blank in reschedule and cancel messages) |
| Appointment date | `{{appointment_date}}` | Thursday, October 8 |
| Appointment time | `{{appointment_time}}` | 9:30 AM |
| Booking page link | `{{booking_url}}` | Your booking page address |
| Patient forms link | `{{forms_url}}` | Your forms link |
| Manage appointment link | `{{appointment_confirmation_url}}` | Opens the reschedule / cancel screen of your booking page |

If a detail is empty — for example no clinic email — a line containing only that detail is left out, so patients never see an empty “Email:” line. Typing an unknown placeholder shows *{{x}} isn't a variable Ordo knows.*

!!! tip "Let patients change their own visit"
    Ordo's default wording does not include the manage link. If your clinic allows online changes, add `{{appointment_confirmation_url}}` to the confirmation and 24-hour reminder, for example: *Need to change it? {{appointment_confirmation_url}}*.

### Text length

Under a text message Ordo shows something like *142 characters · 1 text*. A text holds 160 plain characters; longer messages are split into parts of 153. **Emoji and some special characters** shrink each part to 70 characters, and Ordo tells you when that happens. Shorter texts cost less and arrive in one piece.

### Ordo's default wording

Two examples. The rest follow the same tone.

**Confirmation text**

```text
Hi {{patient_first_name}}, your appointment with {{clinic_name}} is confirmed for {{appointment_date}} at {{appointment_time}} with {{provider_name}}. {{clinic_address}}. Questions? Call {{clinic_phone}}.
```

**24-hour reminder email** — subject *Reminder: Your appointment tomorrow at {{clinic_name}}*

```text
Hi {{patient_first_name}},

This is a friendly reminder about your upcoming appointment.

Appointment details

Date: {{appointment_date}}
Time: {{appointment_time}}
Provider: {{provider_name}}
Reason: {{appointment_type}}
Location: {{clinic_address}}

If you need to make changes, please contact us at {{clinic_phone}}.

See you soon!

{{clinic_name}}
```

---

## Testing mode

Testing mode lets you try the booking page and your messages without messaging real patients.

1. In the **Testing mode** card, enter a **Test email** and/or **Test mobile phone** (US numbers) and click **Save test contacts**.
2. Turn on **Send patient messages to the test contacts**.

While it is on:

- Every confirmation, reminder, and notice goes to the test contacts instead of the patient, with **[Test]** at the start of the subject or text.
- The booking page shows a small banner: *Testing mode: confirmations and reminders from this page go to the clinic's test contacts, not to you.*
- Real patients who book get **no** messages. Turn testing mode off before you share the page.

!!! danger "Bookings are still real"
    Testing mode only redirects messages. Bookings made while it is on are real appointments in Open Dental.

### Send test

In the message editor, **Send test** sends the wording currently in the editor — saved or not, switched on or not — to your test contact. You need a test email (or phone) saved first, and a booking page set up. You can send up to 10 tests every 10 minutes.

---

## Recent messages

The **Testing mode** card lists the 15 most recent messages for the practice:

- date and time;
- which message and channel, and who it went to — masked, for example `j•••@gmail.com` or `•••-•••-1234`;
- a **Test** badge for test sends;
- a status: **Sending**, **Sent**, **Failed**, or **Skipped**, with the reason.

Ordo never stores the message text itself.

| Reason shown | What it means | What to do |
| --- | --- | --- |
| *No email on file* / *No phone on file* | The patient has no email or phone to send to. | Add it in Open Dental for next time. |
| *Testing mode is on but there's no test email* (or phone) | Testing mode has nowhere to send. | Save a test contact, or turn testing mode off. |
| *Email isn't set up yet* | Email is not connected for your clinic. | Email help@perfect.ventures. |
| *Text messages aren't set up yet* | Texts are not connected for your clinic. | Email help@perfect.ventures. |
| *Demo mode: nothing was sent* | You are in Demo mode. | Nothing to do — Demo never sends. |
| **Failed** with an error | The email or text provider refused it (for example an invalid address). Addresses and numbers are hidden in the error. | Check the patient's contact details in Open Dental. If many fail, email help@perfect.ventures. |

---

## Example: Jennifer turns on reminders

Jennifer opens **Clinic settings → Appointments**. In **Testing mode** she saves the front-desk email and her own mobile, and turns testing mode on.

In **Patient messages** she turns on the confirmation (email and text) and the 24-hour reminder (text). She edits the reminder text to add *Need to change it? {{appointment_confirmation_url}}*, checks the preview says *1 text*, and clicks **Send test**. Her phone buzzes with *[Test] Hi Alex, this is a reminder…*.

She makes a test booking on the page. **Recent messages** shows the confirmation as **Sent** with a **Test** badge. She cancels the test visit in Open Dental and turns testing mode off. From now on, patients who book online get a confirmation straight away and a text the day before.

---

## Related pages

- [Online booking page](online-booking.md)
- [Set up online booking](../workflows/set-up-online-booking.md)
- [Appointments](appointments.md)
- [Appointments and booking errors](../errors/appointments.md)
