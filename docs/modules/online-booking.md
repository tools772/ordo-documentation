# Online booking page

The **online booking page** is a web page where patients book their own visit, any time of day. They pick a reason, see real open times from your Open Dental schedule, and confirm. The appointment goes straight into Open Dental, marked so your team knows it came from the web.

Patients can also come back to the same page to **reschedule or cancel** an upcoming visit, if your clinic allows it.

This page explains what patients see, what lands in Open Dental, and the settings your office controls. To get a page live step by step, see [Set up online booking](../workflows/set-up-online-booking.md).

---

## The short version

| Question | Answer |
| --- | --- |
| Where is it? | `https://book.useordo.ai/your-clinic` — you choose the last part. |
| Who sets it up? | Ordo turns on the Appointments module and adds your visit types. Your office picks the web address, name, and time zone, and turns the page on. |
| Where are the settings? | **Clinic settings → Appointments**. |
| Does it write to Open Dental? | Yes. It finds or creates the patient and books the appointment. |
| Does it change insurance plans in Open Dental? | No. Insurance the patient enters goes into the appointment note for your team to verify. |
| Can patients reschedule or cancel? | Only if your clinic allows it (set by Ordo), and not inside the **Patient change cutoff** (24 hours by default). |
| Will patients get emails or texts? | Only the ones you turn on under [Patient messages](patient-messages.md). Nothing is sent by default. |

---

## What patients see

The page shows your logo (or initials), clinic name, address, phone, and email at the top. On a phone there is a call button. At the bottom: *Online booking by Ordo*.

Times are always shown in **your clinic's time zone**, whatever time zone the patient is in.

Booking takes four steps. A progress bar shows where the patient is (**Patient details → Reason for visit → Time slot → Summary**), and they can click back to an earlier step.

### Step 1 — Have you visited us before?

**I'm an existing patient**

The patient enters first name, last name, and birthday, and answers **Has your insurance changed since your last visit?** (Yes shows the insurance fields).

Ordo looks the patient up in Open Dental:

- Last name and birthday must match exactly (accents and punctuation are ignored).
- First name can match the legal name, the preferred name, or the first three or more letters (“Nim” finds “Nimish”).
- Deceased and deleted patients are never matched.

| Result | What the patient sees |
| --- | --- |
| One match | *We found your patient record.* and moves on. |
| A few matches (for example twins, or duplicates) | *We found more than one record with these details. Please choose yours.* Each choice shows only a hint, such as *Phone on file ending in 1234*. |
| No match | *We couldn't find your record…* with an **I'm a new patient** button that carries the details over. |

**I'm a new patient**

First name, last name, birthday, and — depending on your clinic's setup — **Mobile phone**, **Email**, and **Home address** (by default phone and email are asked for). Then **Will you be using dental insurance?**

**Insurance (when the patient says yes)**

- **Insurance company** — a searchable list if your clinic has one (see [Insurance list](#insurance-on-your-booking-page)), with your most common companies first. Companies you do not accept are tagged **Not accepted**; the patient can still book and is told the office will go over payment options. Patients can also type a name that is not listed.
- **Member ID**, **Group number** (optional), **Subscriber name**, **Subscriber birthday**, and **Your relationship to the subscriber** (Self, Spouse, Child, Other).
- **Insurance card and documents** (optional) — up to 5 files, 10 MB each. Usually a photo of the front and back of the card.

!!! note "Refreshing the page"
    For privacy, insurance details and uploaded files are kept only while the page is open. If the patient refreshes, they re-enter them. Progress through the steps is kept for 30 minutes.

### Step 2 — What is your reason to visit?

The patient picks from your **visit types** (for example *New patient exam*, *Cleaning*, *Emergency*). Each type can be shown to everyone, to new patients only, or to existing patients only.

If no visit type fits the patient, they see *Online booking isn't available for this visit type. Please call the office to schedule.*

### Step 3 — What time is convenient for you?

- A strip of seven days with **Previous week** and **Next week**. Days with no openings are greyed out; the first open day is picked for them.
- **Morning** (before noon), **Afternoon** (noon to 5 pm), and **Evening** (5 pm and later).
- Times are grouped under each provider, for example *Dr. Priya Gupta | General Dentist*. Picking a time picks the provider.

**Where the times come from.** Ordo asks Open Dental for open slots the length of the visit, using your provider schedules and operatories. It then keeps only:

- providers and operatories allowed for that visit type;
- dates inside your **booking window** (30 days ahead by default);
- times after your **minimum notice** (2 hours from now by default).

Ordo re-checks the time with Open Dental at the moment the patient confirms.

### Step 4 — Please review the booking details

The patient sees the time, visit type, patient name, provider, and address, and can leave **Information for the doctor** (optional, up to 500 characters). They click **Confirm**.

If someone else took the time a moment earlier, the patient is sent back to pick another (*That time was just booked. Please select another appointment.*). Pressing Confirm twice never books twice.

### Confirmation

*Your appointment is confirmed.* with the clinic, visit type, date, time, provider, and address. **Add to calendar** offers Google Calendar, Apple Calendar, and Outlook. At the bottom: *Need to change something? Call us at {your phone}.*

---

## What lands in Open Dental

1. **The patient.**
    - *Existing patient:* the matched record is used.
    - *New patient:* Ordo first checks for someone with the same name and birthday. If it finds one, it books on that record and flags it for review (see below). Otherwise it creates a new patient with name, birthday, phone, email, address, clinic, and the chosen provider as primary provider.
2. **The appointment** — in the operatory and with the provider of the chosen time, the visit's length, your clinic, the Open Dental appointment type (if Ordo mapped one), and the new-patient flag.
3. **The appointment note**, line by line:

```text
Patient comment: Front tooth sensitive to cold.
Booked online via Ordo (new patient). Ref 3f9a12bc.
Insurance reported online — verify before visit. Carrier: Delta Dental; Member ID: 123456789; Group: 4400; Subscriber: Maria Santos (DOB 03/04/1980, Self); 2 insurance card/document file(s) saved in Ordo.
```

The *Booked online via Ordo* line is what gives the visit its **Booked online** marker in [Appointments](appointments.md).

When a “new” patient matched an existing record, the note also says *Patient chose "new patient" but matched an existing record by name and birthdate — please review.* The new phone or email they typed is **not** written onto the existing record.

!!! warning "Insurance is not entered into Open Dental for you"
    Ordo never creates or changes insurance plans in Open Dental. The details are in the note, and any card photos are under the appointment's **Comments & files** tab in Ordo (marked **From patient**). Verify and enter the plan in Open Dental before the visit.

---

## Rescheduling and cancelling online

When your clinic allows it, step 1 shows *Already have an appointment? Reschedule or cancel it online.* with a **Manage appointment** button. The same screen is reached from the **Manage appointment link** you can put in [patient messages](patient-messages.md).

**Find your appointment.** The patient enters first name, last name, birthday, and **Phone number**. The phone must match a mobile, home, or work number in Open Dental. If nothing matches, they see *We couldn't find an upcoming appointment with those details…* and your phone number. (The same message is used whether or not the person is a patient, to protect privacy.)

**Your upcoming appointments.** Up to 10 scheduled visits in the next year, each with **Reschedule** and/or **Cancel**. This includes **any** upcoming visit in Open Dental, not only ones booked online.

| Situation | What the patient sees |
| --- | --- |
| Inside the cutoff (24 hours by default) | *Changes must be made at least 24 hours before your visit. Please call the office at {phone}.* |
| The provider is not bookable online | *To pick a new time for this visit, please call the office at {phone}.* Cancelling still works. |

**Reschedule.** The patient picks a new time with the **same provider and visit length**, then **Confirm new time**. Open Dental: the appointment moves, and the note gets *Rescheduled online by the patient via Ordo from … to ….*

**Cancel.** The patient can give a reason (optional) and clicks **Cancel appointment**. Open Dental: the appointment is marked **Broken** and moved to the Unscheduled List, and the note gets *Cancelled online by the patient via Ordo. Reason: …*.

Both changes are recorded in your clinic's audit log, and can trigger the **Rescheduled online** and **Cancelled online** [patient messages](patient-messages.md) if you have turned them on.

---

## Settings your office controls

Open **Clinic settings → Appointments**. Viewing needs a role that can open Clinic settings. Changing things needs **Manage team and locations** (the screen calls it *the Manage clinic settings permission*).

The tab has these cards, top to bottom.

### Appointments module (read only)

What Ordo has turned on for your clinic: the module, rescheduling, cancelling, and the patient change cutoff. See [Appointments → What your clinic allows](appointments.md#what-your-clinic-allows).

### Online booking page

| Field | What it does |
| --- | --- |
| **Location** | Shown if you have more than one. *Each location has its own booking page.* |
| **Booking URL** | The last part of the web address, for example `bright-smile`. 3–60 lowercase letters, numbers, and hyphens. Ordo checks it is free as you type (*Available.* / *Already taken. Pick another URL.*). A few words such as `admin`, `book`, and `help` are reserved. |
| **Page name** | Shown at the top of the page. Up to 120 characters. |
| **Time zone** | Eastern, Central, Mountain, Arizona, Pacific, Alaska, or Hawaii. All times on the page use it. |
| **Accept online bookings** | The on/off switch. *When off, the booking URL shows Not found.* |

Buttons: **Create booking page** (first time) or **Save booking page**, **Copy link**, and **Open page**. The badge at the top says **Live**, **Off**, or **Not set up**.

!!! warning "Changing the web address"
    Changing the **Booking URL** breaks every link and website button that used the old one. Ordo warns you before saving. Update your website, Google listing, and any printed QR codes afterwards.

### Website booking button

Shown once the page exists. Ordo writes a small piece of code for your website that opens the booking page in a new tab.

- **Button text** (default *Book an appointment*), **Style** (**Button** or **Text link**), and **Color**.
- A live **Preview**.
- **Copy snippet** copies the code. Paste it into an HTML or embed block on your website, or send it to whoever manages your site. **Copy link only** copies just the address.

### Testing mode and Patient messages

Who gets emails and texts, and what they say. See [Patient messages](patient-messages.md).

### Insurance on your booking page

The list patients choose from in the insurance step. It is shared by every location in the practice.

- **Load the standard list** adds about 250 common US dental insurance companies, all marked Accepted.
- **Add an insurance company** adds your own (up to 1,000 in total).
- Each row has a **star** (*Show first on the booking page*), an **Accepted / Not accepted** switch, and a delete button.
- Search and filter by **All**, **Accepted**, **Not accepted**, or **Most common**.

With an empty list, patients simply type their insurance company.

### Settings Ordo sets for you

These are not on screen yet. Email **[help@perfect.ventures](mailto:help@perfect.ventures)** to change them:

| Setting | Default |
| --- | --- |
| **Visit types** (name, description, length, new / existing / everyone, which providers and operatories) | None — a new page needs at least one before patients can book |
| Which providers appear, and their display names and specialties | Every provider that is not hidden in Open Dental |
| Booking window | 30 days |
| Minimum notice | 2 hours |
| Fields asked of new patients | Phone and email |
| Insurance card upload | On |
| Logo, brand colour, clinic email for replies, “In-network” label | None |

---

## Testing before you share the link

Turn on **Testing mode** (see [Patient messages](patient-messages.md#testing-mode)). The page shows a small banner, and every confirmation and reminder goes to your test email and phone instead of the patient.

!!! danger "Test bookings are real bookings"
    Testing mode only changes **where messages go**. A test booking still creates a real patient (if new) and a real appointment in Open Dental. Use a test patient name you will recognise, then cancel the visit — and remove the test patient — in Open Dental afterwards.

---

## Example: Bright Smile goes live

Sarah (Owner) asks Ordo to turn on Appointments and add three visit types: *New patient exam* (new patients, 60 min), *Cleaning* (existing patients, 60 min), and *Emergency* (everyone, 30 min).

Jennifer opens **Clinic settings → Appointments**, types `bright-smile` as the **Booking URL**, sets **Pacific** time, and clicks **Create booking page**. She clicks **Load the standard list** under insurance and stars Delta Dental, MetLife, and Cigna.

She turns on **Testing mode** with the front-desk email, books a test visit as “Test Patient”, checks the visit in Open Dental (note says *Booked online via Ordo*), and cancels it. She turns Testing mode off, copies the **Website booking button** snippet, and sends it to the web designer.

On Monday morning, Appointments shows two new visits with a globe icon.

---

## Related pages

- [Set up online booking](../workflows/set-up-online-booking.md)
- [Patient messages](patient-messages.md)
- [Appointments](appointments.md)
- [Appointments and booking errors](../errors/appointments.md)
- [Clinic settings](clinic-settings.md)
