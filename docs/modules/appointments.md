# Appointments

**Appointments** is your Open Dental schedule inside Ordo. The front desk can see the day or week, find a patient, book someone who is on the phone, move or cancel a visit, and leave notes and files for the team — without switching to Open Dental for every small job.

Ordo does not keep its own copy of the schedule. Every time you open the page, Ordo reads it from Open Dental. Anything you change here (a new time, a cancellation, a colour) is written straight back to Open Dental, so the whole office sees the same thing.

Open it from the sidebar: **Appointments** (calendar icon), under **Modules**.

---

## Before you can use it

Three things have to be true. If one is missing, the page tells you which.

| What | Who sets it | What you see if it is missing |
| --- | --- | --- |
| **The module is on for your clinic** | Ordo turns it on during onboarding. | No **Appointments** item in the sidebar. If you open the link anyway: *Appointments isn't enabled for this clinic*. |
| **Your role can see the schedule** | An Owner or Admin, under **Clinic settings → Profile → Roles**. | No sidebar item. Opening the link sends you to a “no access” page. |
| **This location is connected to Open Dental** | Your office, under **Clinic settings → PMS Integrations**. | *Connect Open Dental to see appointments*, with an **Open clinic settings** button. **Book appointment** is greyed out. |

You can check whether the module is on, and what your clinic allows, under **Clinic settings → Modules** or **Clinic settings → Appointments**. The **Appointments module** card there is marked **Managed by Ordo**. You can read it but not change it. To change it, email **[help@perfect.ventures](mailto:help@perfect.ventures)**.

### What your clinic allows

Ordo sets these for your clinic. They apply to everyone, whatever their role.

| Setting on the card | Plain meaning |
| --- | --- |
| **Appointments** | The module is on, and roles that include it can see the schedule. |
| **Clinic allows rescheduling** | Staff can move appointments into open times. Patients can also reschedule from your [online booking page](online-booking.md). |
| **Clinic allows cancelling** | Staff can cancel. A cancelled visit is marked **Broken** in Open Dental and moved to the Unscheduled List. Patients can also cancel online. |
| **Patient change cutoff** (hours) | Patients cannot reschedule or cancel online closer to the visit than this (default 24 hours). **Staff are never blocked.** |

### Who can do what

Your role decides what you can do. The permissions sit under **Appointments** in the role editor:

| Permission (role editor label) | What it unlocks | Starter roles that have it |
| --- | --- | --- |
| **View schedule** | See the page, open any appointment, read comments and files. | Owner, Admin, Reviewer, Viewer |
| **Edit details** | Change the appointment colour, add comments, attach and remove files. | Owner, Admin |
| **Reschedule and cancel** | **Book appointment**, **Reschedule**, and **Cancel** (rescheduling and cancelling only when your clinic allows them). | Owner, Admin |

The **Patient** tab inside an appointment also needs the **View patients** permission. More on roles: [Roles and who can do what](../people/roles.md).

!!! tip "If a button is missing"
    No **Reschedule** button usually means your clinic does not allow rescheduling, or your role lacks **Reschedule and cancel**. The card under **Clinic settings → Appointments** shows which. Completed and broken visits never show Reschedule or Cancel.

---

## The page at a glance

```
 ┌─────────────────────────────────────────────────────────────┐
 │ Appointments                   [Export .ics] [Book appointment]
 ├─────────────────────────────────────────────────────────────┤
 │ ‹ Today ›  [Wed, Oct 7, 2026]     Day | Week | List   ⟳     │
 │ Search…  Provider ▾  Status ▾  Booked via ▾  Insurance ▾    │
 ├─────────────────────────────────────────────────────────────┤
 │ Appointments · Scheduled · Completed · Broken ·             │
 │ Booked online · Booked on call                              │
 ├─────────────────────────────────────────────────────────────┤
 │ the schedule: Day grid, Week grid, or List                  │
 └─────────────────────────────────────────────────────────────┘
```

### Header buttons

| Button | What it does |
| --- | --- |
| **Export .ics** | Downloads the appointments you are looking at as a calendar file. See [Export to a calendar](#export-to-a-calendar-ics). |
| **Book appointment** | Book a patient who is on the phone or at the desk. Only shown if your role can reschedule and cancel. See [Book an appointment on a call](../workflows/book-by-phone.md). |

### Moving around the calendar

- **‹** and **›** move one day in Day view, or one week in Week and List views. **Today** jumps back to today.
- Click the **date** to pick any day from a calendar.
- **Day | Week | List** switches the view. While the new view loads, the button shows a small spinner and the page shows *Loading week view…* (or day, or list).
- **⟳ Refresh schedule** reads Open Dental again straight away.

The web address keeps your view and date, so you can bookmark *this week in List view* or send the link to a colleague. Filters are not saved in the link and reset when the page reloads.

**How fresh is it?** When you are looking at a range that includes today, Ordo re-reads Open Dental every two minutes and whenever you come back to the browser tab. A change made in Open Dental shows up within about two minutes, or immediately if you click Refresh. A brand-new provider or operatory can take up to five minutes to appear.

### Filters

| Filter | Choices | Notes |
| --- | --- | --- |
| **Search patient or procedure** | Type any part of a name or procedure. | Does not search the appointment note. |
| **Provider** | **All providers**, then each active Open Dental provider. | A hidden provider appears only while they have visits in the range. |
| **Status** | **All statuses**, **Scheduled**, **Completed**, **Broken** | See [Statuses](#statuses-and-markers). |
| **Booked via** | **All bookings**, **Booked online**, **Booked on call** | Only finds visits booked through Ordo. |
| **Insurance** | **All insurance**, each insurance company on the schedule (with a patient count), **No insurance on file** | Matches primary or secondary plan. Loads a moment after the schedule. |

**Clear** resets every filter at once.

!!! note "Insurance filter"
    Spelling variants are grouped (“METLIFE” and “MetLife” are one choice). Medical plans are ignored. Ordo remembers insurance for 30 minutes, so a plan you just changed in Open Dental can take that long to show here. If some patients could not be checked, hover the filter to see how many.

### The stat cards

Six cards sit above the schedule: **Appointments** (the total), **Scheduled**, **Completed**, **Broken**, **Booked online**, and **Booked on call**.

- The counts always cover the **whole date range**. They do not change when you filter.
- **Booked online** and **Booked on call** are clickable. Click one to show only those visits; click again to show everything. The active card gets a coloured outline.

If Open Dental could not return some patient names, a line under the cards says so, and those rows show as **Patient #1234**. Refresh usually fixes it.

---

## The three views

### Day

One column per **operatory** (chair), in the same order as Open Dental, with each column's appointment count at the top. When you filter, only operatories with matching visits stay on screen.

### Week

Sunday to Saturday, one column per day. Today's column is tinted. **Click a day's heading** to open that day in Day view.

In both calendar views:

- The grid shows 7 am to 6 pm and stretches if there are earlier or later visits.
- On today, a **red line** marks the current time, and the page scrolls to just before it.
- Overlapping visits sit side by side.
- Each block shows the patient name, start time, check-in state (for example *· In chair*), and procedures. Small icons mark visits booked through Ordo (globe = online, phone = on a call), **NP** marks a new patient, and counts show comments and files.

### List

A table of the **same Sunday-to-Saturday week** as Week view — handy for calling down a list or scanning for unconfirmed visits.

| Column | What is in it |
| --- | --- |
| **Time** | Start time. |
| **Patient** | Name, **NP** for new patients, an **Online · Ordo** or **On call · Ordo** badge, and comment and file counts. |
| **Procedures** | What is planned. |
| **Insurance** | Primary insurance company, with **+1** (and so on) if there are more. Hover to see all of them. |
| **Provider** | Who the visit is with. |
| **Operatory** | Which chair. |
| **Status** | Scheduled, Completed, or Broken, plus *Arrived*, *In chair*, or *Dismissed*. |
| **Confirmation** | Your clinic's own Open Dental confirmation label (for example *Confirmed*, *Left Msg*). A dash means not set. |

**Sorting.** Click a column heading to sort by it; click again to reverse. You can sort by Time, Patient, Provider, Operatory, Status, and Confirmation. Status sorts Scheduled → Completed → Broken. Blank confirmations always go to the bottom. The default is Time, earliest first.

When sorted by **Time**, rows are grouped under a heading for each day, for example *Wed, Oct 7 · 12 appointments*. Sorted any other way, the date appears in front of the time instead.

**Pages.** The footer shows something like *1–25 of 80*. Choose **Rows per page** (25, 50, or 100) and use **‹ ›** to page through. Changing the dates or a filter goes back to page 1.

---

## Statuses and markers

| Ordo shows | Open Dental status | Meaning |
| --- | --- | --- |
| **Scheduled** (blue) | Scheduled or ASAP | An upcoming or same-day visit. ASAP visits also get an **ASAP** chip. |
| **Completed** (green) | Complete | The visit happened and was set complete in Open Dental. |
| **Broken** (rose, name struck through) | Broken | The patient did not come, or the visit was cancelled. It stays on the schedule so you can see the gap. |

Planned and Unscheduled List items are not shown on the schedule.

**Check-in** (*Arrived*, *In chair*, *Dismissed*) comes from the times recorded in Open Dental. **Confirmation** is your Open Dental confirmation label. Ordo shows both but cannot change them — do that in Open Dental.

**Booked through Ordo.** Ordo marks visits it booked:

| Marker | Meaning |
| --- | --- |
| Globe icon · **Online · Ordo** · *Booked online* | The patient booked on your [online booking page](online-booking.md). |
| Phone icon · **On call · Ordo** · *Booked on call* | Someone on your team booked it in Ordo while on a call with the patient. |

Ordo recognises these from a line it writes into the Open Dental appointment note (*Booked online via Ordo* or *Booked by phone in Ordo*). If someone deletes that line in Open Dental, the marker disappears. Visits booked directly in Open Dental have no marker, even if the patient phoned.

**Colours.** Blocks are tinted by status. If a colour is set on the appointment (in Ordo or in Open Dental), that colour wins and also shows as a dot next to the name.

---

## Inside an appointment

Click any block or row. A panel opens on the right.

The top shows the patient, the date and time with length (for example *Wed, Oct 7 · 9:00 am – 10:00 am (1 hr)*), and chips for status, check-in, **New patient**, **ASAP**, and how it was booked. **Scheduled** visits also show **Reschedule** and **Cancel** if you are allowed to use them.

The panel has up to three tabs.

### Details

- **Colour** — pick **Default**, one of nine colours, or **Custom colour**. Saved on the appointment in Open Dental, so the whole team sees it. Needs **Edit details**.
- **Procedures**, **Provider**, **Hygienist** (if any), **Operatory**, **Insurance** (each plan labelled Primary, Secondary…), **Confirmation**, and **Visit type** (Hygiene or Doctor).
- A line explaining how it was booked, if Ordo booked it.
- **Appointment note** — the full Open Dental note, read only.
- At the bottom, the Open Dental appointment and patient numbers, for when you need to find it in Open Dental.

### Patient

Read-only details from Open Dental. Needs the **View patients** permission.

- A red banner if **Premedication required** or a medical alert is set.
- Name, preferred name, age, birthdate, gender.
- **Contact** — phones (click to call), email, address, and contact preference, including *OK to text* or *Do not text*.
- **Practice** — patient status, patient since, primary provider, whether insurance is on file, billing type.
- **Balance** — total, insurance estimate, patient estimate.

Ordo never shows the Social Security number.

### Comments & files

A shared space for the team, stored in Ordo. Everyone who can see the schedule can read it; you need **Edit details** to add or remove things.

**Comments**

- Type in **Add a comment for the team…** (up to 2,000 characters) and click **Add comment**, or press Ctrl+Enter (Cmd+Enter on a Mac).
- Comments stay in Ordo unless you tick **Also add to the Open Dental appointment note**. Then Ordo also adds *Comment in Ordo by {your name}: …* to the note (the first 1,000 characters).
- You can delete your own comments with the bin icon. Deleting does not remove text already copied into Open Dental.

**Files**

- Drop files on the box or click **Attach files**. Accepted: PDF, images, Word, Excel, PowerPoint, text, CSV, or ZIP, up to 10 MB each and 10 at a time.
- Files are stored in Ordo, **not** in Open Dental's document imaging.
- Files a patient uploaded on the booking page (for example an insurance card) show a **From patient** chip.
- **Download** opens a short-lived link. **Remove** deletes the file straight away, with no undo.

!!! warning "Keep it about the visit"
    Comments and files are visible to everyone who can see the schedule. Ordo's audit log records who added, downloaded, or removed what, but never the comment text or file contents.

---

## Reschedule

1. Open a **Scheduled** appointment and click **Reschedule**.
2. Choose the **Day** (arrows or the date picker; past days are blocked).
3. Choose the **Provider**. It starts on whoever the visit is booked with.
4. Under **Open times**, pick a time. Times come from Open Dental's open-slot search, on 15-minute steps, grouped by operatory, and only where the whole visit fits.
5. Check the line at the bottom — *Move to Oct 9, 2026 at 9:00 am in Op 2 with Dr. Smith* — and click **Confirm new time**.

Ordo checks the time is still free, moves the appointment in Open Dental, and adds a line to the note: *Rescheduled in Ordo by {you} from … to ….* The visit keeps its length. If someone grabbed the time in the meantime, you will see *That time is no longer open. Pick another time.* and the list refreshes.

Moving a hygiene visit to another hygienist keeps the patient's dentist.

## Cancel

1. Open a **Scheduled** appointment and click **Cancel**.
2. Optionally type a **Reason** (up to 300 characters). It is added to the Open Dental note.
3. Click **Cancel appointment**. To back out, click **Keep appointment**.

In Open Dental the appointment is marked **Broken** and moved to the **Unscheduled List**, so the office can follow up. **No broken-appointment fee is posted.** The note gets *Cancelled in Ordo by {you}. Reason: …*. The visit stays on the Ordo schedule, struck through.

Ordo cannot restore a broken appointment. Do that in Open Dental.

!!! note "Messages to the patient"
    Staff reschedules and cancellations do not send the patient a message. If the visit was booked online, its reminders follow the change: a cancelled visit gets no reminder, and a moved visit is reminded at the new time. See [Patient messages](patient-messages.md).

---

## Export to a calendar (.ics)

**Export .ics** downloads exactly what you are looking at — the current dates **and** filters — as a calendar file you can open in Google Calendar, Apple Calendar, or Outlook. In List view it includes every page, not just the one on screen.

| What | Value |
| --- | --- |
| File name | `ordo-schedule-2026-10-07.ics` for one day, or `ordo-schedule-2026-10-04-to-2026-10-10.ics` for a week |
| Event title | *Patient — procedures* |
| Event location | The operatory |
| Event details | Procedures, provider, hygienist, operatory, status and check-in, confirmation, how it was booked, *New patient*, and the Open Dental appointment number |
| Broken visits | Exported as cancelled events |

Times are your clinic's clock times, so a 9:00 am visit shows at 9:00 am in the calendar app.

!!! warning "Appointment notes are left out on purpose"
    Notes can hold insurance member IDs and other private details, so they are never exported. Treat the file like any other patient list: do not email it outside the practice.

---

## What Ordo cannot do here (yet)

Do these in Open Dental:

- Change confirmation status or check someone in.
- Edit procedures, or edit the note directly (Ordo can only add lines to it).
- Drag and drop appointments, or change a visit's length when rescheduling.
- Restore a broken appointment.
- Book in the past.

---

## Example: a Tuesday at Bright Smile

Jennifer opens **Appointments** at 7:45 am. Day view shows the red “now” line just above the first patients. She filters **Status → Scheduled** and switches to **List**, sorted by **Confirmation**, so the unconfirmed visits sit at the bottom. She works down the list by phone.

Maria Santos calls: she cannot make Thursday. Jennifer opens Maria's visit, clicks **Reschedule**, picks next Monday with the same hygienist, and clicks **Confirm new time**. Open Dental now shows the new time, with a note saying Jennifer moved it.

Later, a new patient calls to book. Jennifer clicks **Book appointment** and follows [Book an appointment on a call](../workflows/book-by-phone.md). The visit appears on the schedule with a phone icon.

Mike (Reviewer) can see the whole schedule and read the team's comments, but has no Reschedule or Cancel buttons. That is his role working as designed.

---

## Related pages

- [Book an appointment on a call](../workflows/book-by-phone.md)
- [Online booking page](online-booking.md)
- [Patient messages](patient-messages.md)
- [Appointments and booking errors](../errors/appointments.md)
- [Clinic settings](clinic-settings.md)
- [Roles and who can do what](../people/roles.md)
