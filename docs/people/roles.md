# Roles and who can do what

A **role** is a nametag that turns modules and buttons on or off. Two people can work the same EOB and see different buttons. That is intentional.

Owners and Admins manage roles in **Clinic settings → Profile** (team and roles section).

---

## The four starter roles

| Role | Meant for | Can post? | Can invite staff? |
| --- | --- | --- | --- |
| **Owner** | Practice owner / responsible party | Yes | Yes |
| **Admin** | Office manager who runs posting day to day | Yes | Yes |
| **Reviewer** | Insurance coordinator who checks matches | No | No |
| **Viewer** | Shadow, accountant, dentist who only looks | No | No |

The **Owner** role is a system role. You cannot delete it, and the last remaining owner cannot be demoted.

Admins start with the same clinic abilities as owners in the default setup (upload, review, post, manage team). You can narrow an Admin clone later if you want.

---

## Permission catalog (clinic)

The role editor groups permissions by area. Labels below match the screen.

### EOBs

| Permission | What it unlocks |
| --- | --- |
| View dashboard | See uploaded EOBs and open a file |
| Upload | Upload new EOB files |
| Archive | Archive or restore EOBs and patients |
| Edit extracted data | Change patient details and procedure lines |

### Patients

| Permission | What it unlocks |
| --- | --- |
| View queue | See the cross-file patient list |
| Link OD patient | Confirm or clear the Open Dental patient link |

### Matching

| Permission | What it unlocks |
| --- | --- |
| Run matching | Compute or refresh Open Dental claim matches |
| Fetch Open Dental | Pull Open Dental chart data for patients on an EOB |
| Approve match | Confirm an Open Dental claim match |
| Reject match | Discard a candidate without posting |

### Payments

| Permission | What it unlocks |
| --- | --- |
| Post payment | Write `InsPayAmt` to Open Dental |

### Analytics

| Permission | What it unlocks |
| --- | --- |
| View analytics | Posting Analytics, Payment Analytics, and Fee Analysis |
| Analytics AI chat | The Analytics AI page |
| Fetch schedules | Schedule automatic Historical and Missing Posting data fetches |

### Appointments

Only matter when Ordo has turned on the Appointments module for your clinic.

| Permission | What it unlocks |
| --- | --- |
| View schedule | See the Appointments page, open appointments, read comments and files |
| Edit details | Change appointment colour, add comments, attach and remove files |
| Reschedule and cancel | Book appointments on a call, and reschedule or cancel when your clinic allows it |

The **Patient** tab inside an appointment also needs **View patients**. Details: [Appointments](../modules/appointments.md#who-can-do-what).

The **Payment Analysis** tab inside an EOB comes with **View dashboard** — it does not need **View analytics**. Recording a decision there (**Review**) needs **Edit extracted data**.

### Clinic settings

| Area | Permission | What it unlocks |
| --- | --- | --- |
| Team & locations | View | Open practice settings |
| Team & locations | Manage | Create roles, assign users, edit locations and clinic profile |
| Insurance | Manage formats | Enable catalog formats, aliases, and clinic sample EOBs |
| Fee schedules | Manage | Upload and edit fee schedules and date maps |
| PMS integrations | Manage | Connect Open Dental, save keys, and run clinic-wide sync |

---

## What each starter role can do

| Ability | Owner | Admin | Reviewer | Viewer |
| --- | --- | --- | --- | --- |
| See dashboard, patients | Yes | Yes | Yes | Yes |
| See Analytics (and Analytics AI) | Yes | Yes | No* | Yes |
| Upload / archive | Yes | Yes | No | No |
| Edit extracted data | Yes | Yes | Yes | No |
| Fetch, run matching, link patient | Yes | Yes | Yes | No |
| Approve / reject match | Yes | Yes | Yes | No |
| Post payment | Yes | Yes | No | No |
| See the appointment schedule | Yes | Yes | Yes | Yes |
| Appointment colour, comments, files | Yes | Yes | No | No |
| Book, reschedule, cancel appointments | Yes | Yes | No | No |
| Open Clinic settings | Yes | Yes | No | No |
| Manage team, fee schedules, formats, Open Dental connection | Yes | Yes | No | No |

\*Default Reviewer does **not** include Analytics. If your coordinators should see the numbers, clone Reviewer and tick **View analytics** (and **Analytics AI chat** if they want it).

---

## Bright Smile stories

### Mike (Reviewer) — “I cannot post”

Mike opens Maria Santos, fetches, approves. **Post payment** is missing. Jennifer (Admin) opens the same patient and posts. This is the two-person control Bright Smile wanted.

If the office later decides Mike should post, Sarah clones Reviewer, names it **Poster**, ticks **Post payment** (and maybe **Upload EOBs**), and assigns Mike that role. No software developer is required.

### Alex (Viewer) — “I only wanted to watch”

Alex can open Posting Analytics for the owner meeting, or ask Analytics AI a question. He cannot archive a file, cannot approve, cannot post. If a button is missing, he should not hunt for a bug.

### Priya — custom “Insurance poster”

Sarah wants someone who can upload and post but **cannot** invite users or change roles:

1. Clone **Admin**.
2. Under **Clinic settings**, untick every **Manage** box (team & locations, formats, fee schedules, PMS integrations).
3. Save as **Insurance poster**.
4. Assign Priya.

Priya still sees Clinic settings if **Team & locations → View** is ticked, but she cannot rewrite the team or change fee schedules.

---

## Locations and roles together

A user can be Admin and still “see nothing” if they are mapped to **North Clinic** and today’s files belong to **Main Street**, depending on how your practice uses locations. When access looks random, check **location mapping** before changing roles.

---

## Related pages

- [Clinic settings](../modules/clinic-settings.md)
- [Analytics](../modules/analytics.md)
- [Post a payment](../workflows/posting-a-payment.md)
