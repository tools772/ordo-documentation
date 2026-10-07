# Set up online booking

A checklist for getting your [online booking page](../modules/online-booking.md) live, from first request to the button on your website. Plan about 30 minutes of your time, plus a short back-and-forth with Ordo.

**You need:** a role with **Manage team and locations** (to edit Clinic settings), and Open Dental connected for the location under **Clinic settings → PMS Integrations**.

---

## 1. Ask Ordo to turn it on

Email **[help@perfect.ventures](mailto:help@perfect.ventures)** with:

- **Which locations** should have a booking page.
- **Your visit types.** For each: the name patients see, a one-line description, the length, and whether it is for new patients, existing patients, or everyone. For example *New patient exam — 60 min — new patients*, *Cleaning — 60 min — existing patients*, *Emergency visit — 30 min — everyone*.
- **Which providers** patients can book with, and how their names should appear (for example *Dr. Priya Gupta — General Dentist*). By default every provider who is not hidden in Open Dental is offered.
- Whether patients may **reschedule** and/or **cancel** online, and how close to the visit they must stop (24 hours by default).
- Optional: your **logo**, **brand colour**, a **clinic email** for replies, how far ahead patients can book (30 days by default), and how much notice you need (2 hours by default).

Ordo turns on the **Appointments** module and adds your visit types. You can confirm under **Clinic settings → Appointments**: the **Appointments module** card shows **On**.

!!! tip "Open Dental schedules drive the times"
    Patients only see times where your **provider schedules** in Open Dental have openings. If a provider has no schedule set up in Open Dental for next week, they show no times online. Check provider schedules before going live.

## 2. Create the page

1. Open **Clinic settings → Appointments**.
2. In **Online booking page**, pick the **Location** (if you have more than one).
3. Type a **Booking URL**, for example `bright-smile`. Wait for *Available.*
4. Check the **Page name** and **Time zone**.
5. Click **Create booking page**.

The badge changes to **Live**. Click **Open page** to see it as a patient would.

## 3. Add your insurance list (optional, recommended)

In **Insurance on your booking page**:

1. Click **Load the standard list**.
2. Switch off the companies you do **not** accept. Patients will see **Not accepted** next to them before they book.
3. Star the three to five companies most of your patients have, so they show first.
4. Add any local plans with **Add an insurance company**.

## 4. Choose your patient messages

In **Patient messages**, turn on what you want patients to receive. A good starting set:

- **Appointment confirmation** — email and text.
- **Appointment reminder, 24 hours before** — text.
- **Forms reminder** — email, if you have online forms (save the **Forms link** first).

Check the wording with **Edit**. Details: [Patient messages](../modules/patient-messages.md).

## 5. Test it

1. In **Testing mode**, save a test email and mobile, and turn on **Send patient messages to the test contacts**.
2. Open your booking page and book as a **new patient** called *Test Patient*.
3. Check:
    - the visit is in Open Dental, with *Booked online via Ordo* in the note;
    - it shows on the Ordo **Appointments** page with a globe icon;
    - **Recent messages** shows the confirmation as **Sent**, with a **Test** badge, and it arrived on your test phone or email.
4. If your clinic allows online changes, try **Manage appointment** on the booking page with the test patient's name, birthday, and phone, and reschedule.
5. In Open Dental, cancel the test visit and remove the test patient.
6. **Turn testing mode off.**

!!! danger "Test bookings are real"
    Testing mode only redirects messages. The test patient and visit are real in Open Dental until you remove them.

## 6. Share the link

- **Website:** in **Website booking button**, set the button text and style, click **Copy snippet**, and paste it into your site (or send it to your web designer).
- **Everywhere else:** **Copy link** for Google Business Profile, Facebook, email signatures, and your phone greeting.

---

## After you go live

- Online bookings show on **Appointments** with a globe icon. Filter **Booked via → Booked online** to see them all.
- Read the appointment note on each online booking. **Verify insurance** in Open Dental before the visit — Ordo puts what the patient typed in the note but does not create the plan.
- Look out for notes saying *matched an existing record… please review*; a “new” patient was actually already in your system.
- Check **Recent messages** now and then for **Failed** or **Skipped** messages.
- To pause online booking, switch off **Accept online bookings**. The link then shows *Online booking isn't available here*.

---

## Related pages

- [Online booking page](../modules/online-booking.md)
- [Patient messages](../modules/patient-messages.md)
- [Appointments](../modules/appointments.md)
- [Appointments and booking errors](../errors/appointments.md)
