# Book an appointment on a call

Use this when a patient phones or walks up to the desk. You book in Ordo, and the appointment goes straight into Open Dental with an **On call** marker so the team knows it was booked by phone.

**You need:** the Appointments module on for your clinic, a role with **Reschedule and cancel**, and Open Dental connected for your location. See [Appointments → Before you can use it](../modules/appointments.md#before-you-can-use-it).

---

## Step 1 — Choose the patient

Open **Appointments** and click **Book appointment** (top right). Choose **Existing patient** or **New patient**.

### Existing patient

1. Type at least two letters of the **Last name**. Add **First name** and **Date of birth** (MM/DD/YYYY) to narrow the list. Click **Search**.
2. Pick the patient. Each result shows the birthdate and the last four digits of their phone, so you can confirm with the caller. A chip such as **Inactive** appears if the patient is not active.

If nobody comes up: *No patients found. Check the spelling or add them as a new patient.*

### New patient

1. Enter **First name**, **Last name**, and **Date of birth**. **Mobile phone** and **Email** are optional but help later.
2. Click **Continue to times**.

Before adding the patient, Ordo checks Open Dental for someone with the same name and birthdate. If it finds one, it stops with *A patient with this name and date of birth is already in Open Dental. Search for them under Existing patient.* That protects you from creating a duplicate chart.

Staff booking does not ask for address or insurance. Add those in Open Dental.

## Step 2 — Pick a time

1. Choose the **Visit length** (15 minutes to 2 hours; 1 hour by default).
2. Choose the **Day** and the **Provider**.
3. Under **Open times**, pick a time. Times come from Open Dental's open-slot search and are grouped by operatory.
4. Optionally type a **Reason for visit** (up to 500 characters). It goes into the Open Dental note.
5. Check the summary — *Book Oct 8, 2026 at 10:40 am in Op 1 with Dr. Gupta* — and click **Book appointment**.

Ordo checks the time is still free and books it. You see *Booked Maria Santos for Oct 08, 2026 at 10:40 am*, and the schedule jumps to that day.

---

## What is written to Open Dental

- **New patient only:** a patient record with name, birthdate, mobile phone, email, clinic, and primary provider.
- **The appointment:** patient, operatory, time, length, provider (and hygienist for hygiene times), clinic, and the new-patient flag. Procedures and confirmation status are left blank — fill them in Open Dental if your office uses them.
- **The note:**

```text
Reason: Broken filling, lower left.
Booked by phone in Ordo by Jennifer Park (new patient).
```

The second line is what shows the **On call · Ordo** marker on the schedule.

!!! note "No message to the patient"
    Ordo does not send confirmations or reminders for visits booked on a call. Use your usual Open Dental reminders for these patients. See [Patient messages](../modules/patient-messages.md).

---

## If something goes wrong

| Message | What to do |
| --- | --- |
| *That time is no longer open. Pick another time.* | Someone booked it a moment ago. Pick another time. |
| *A patient with this name and date of birth is already in Open Dental…* | Switch to **Existing patient** and search. |
| *The patient was added to Open Dental, but the appointment could not be booked…* | The chart exists now. Search under **Existing patient** and book again — do not add them a second time. |
| *Enter at least 2 letters of the last name.* | Type more of the name. |
| *Open Dental is not connected…* | Ask an Owner or Admin to check **Clinic settings → PMS Integrations**. |

More: [Appointments and booking errors](../errors/appointments.md).

---

## Example

A new patient, Daniel Kim, calls Bright Smile about a chipped tooth. Jennifer clicks **Book appointment → New patient**, types *Daniel Kim*, *05/12/1991*, and his mobile, and clicks **Continue to times**. She picks **30 min**, tomorrow, **Dr. Gupta**, and the 10:40 am time in Op 1, types *Chipped front tooth* as the reason, and clicks **Book appointment**.

Open Dental now has Daniel's chart and a 30-minute visit with the note *Reason: Chipped front tooth / Booked by phone in Ordo by Jennifer Park (new patient).* On the Ordo schedule it shows a phone icon and **NP**.

---

## Related pages

- [Appointments](../modules/appointments.md)
- [Online booking page](../modules/online-booking.md)
- [Roles and who can do what](../people/roles.md)
