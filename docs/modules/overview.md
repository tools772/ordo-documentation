# What is a module?

A **module** is one section of Ordo — a room with a job. The left sidebar lists the rooms your role can enter. This page is the floor plan. Each module has its own longer page with examples.

---

## Why the product is split this way

Insurance posting is a pipeline:

**File arrives → people are read off the page → someone matches them to the chart → someone posts → someone checks the numbers later.**

Each module is one stage of that pipeline (plus settings):

```
  Upload PDF          Find a person           Check the numbers
       │                    │                         │
       ▼                    ▼                         ▼
 EOB Dashboard  ←──  Patients list  ──→  Analytics
       │                                  (Posting · Payment ·
       ▼                                   Fee Analysis · AI)
  Open one file
  (Posting / Payment Analysis;
   per patient: EOB Review / Payment Analysis /
   Open Dental / Audit)
       │
       ▼
  Clinic settings (people, Open Dental connection, fee schedules)
```

Alongside that pipeline sits the front desk:

```
  Patient books online ──┐
  Patient calls ─────────┼──→  Appointments  ──→  Open Dental schedule
  Visit moves / cancels ─┘     (Day · Week · List)
                                     │
                                     ▼
                          Patient messages (confirmations, reminders)
```

You do not have to visit every room every day. Many coordinators live in **EOB Dashboard**; the front desk lives in **Appointments**. The office manager dips into **Analytics** on Friday. The owner opens **Clinic settings** when a new hire starts or a new insurance contract arrives.

---

## The sidebar, group by group

### Modules (daily work)

| Menu label | Job in one sentence | Typical visitor |
| --- | --- | --- |
| **EOB Dashboard** | Inbox of remittance files. | Everyone who posts or reviews. |
| **Patients** | All extracted people, across files, plus EOB history on the person. | “Where is this patient?” questions. |
| **Appointments** | The Open Dental schedule: book, reschedule, cancel, comment, export. Only shown when Ordo has turned it on for your clinic. | Front desk, office manager. |
| **Analytics** | A collapsible group with four pages (below). | Office manager, owner, billing lead. |

Details: [Appointments](appointments.md). Patients book themselves on the [online booking page](online-booking.md), and get [patient messages](patient-messages.md) you choose.

Inside **Analytics**:

| Menu label | Job in one sentence |
| --- | --- |
| **Posting Analytics** | Uploaded / posted / failed counts (**Overview**, formerly Reports), plus claims in Open Dental with nothing posted (**Missing Posting**). |
| **Payment Analytics** | Underpayments against your contracted fees — on uploaded EOBs (**Remittances**) and on past Open Dental claims (**Historical Analysis**). |
| **Fee Analysis** | Contracted fees side by side with your office UCR, for any date. |
| **Analytics AI** | Ask analytics questions in plain English. |

Details: [Analytics](analytics.md).

### Practice

| Menu label | Job in one sentence | Typical visitor |
| --- | --- | --- |
| **Clinic settings** | Team, roles, locations, Open Dental connection, insurance formats, fee schedules, modules, booking page and patient messages, logs. | Owner, clinic admin. |

At the bottom of the sidebar: **Help & docs** (this site), the support email, and the **App mode** switch (Demo / Actual).

If a menu item is missing, that is normal. Your role only shows the rooms you are allowed to enter, and some modules (Appointments, and individual Analytics pages) only appear once Ordo has turned them on for your clinic. **Clinic settings → Modules** shows which are on.

---

## Example: who uses which rooms at Bright Smile

Bright Smile Dental has four people in the demo story:

| Person | Role | Modules they live in |
| --- | --- | --- |
| **Sarah Chen** | Owner | Everything clinic-side. She sets roles and fee schedules, glances at Analytics on Monday, rarely posts. |
| **Jennifer Park** | Admin | Dashboard (upload + post), Payment Analytics (underpayments), Clinic settings (invite staff). |
| **Mike Johnson** | Reviewer | Dashboard and the Open Dental tab. He approves and rejects. He cannot post, cannot change settings, and does not see Analytics by default. |
| **Alex Rivera** | Viewer | Dashboard, Patients, Analytics — read only. Useful for a new hire shadowing, or an accountant who should not click Post. |

If Alex opens an EOB, he can read Maria Santos’s lines. He will not see **Post payment**. That is the product working as designed, not a broken button.

---

## What “you cannot see this” usually means

Three common reasons:

1. **Role.** Your permission set does not include that module or button. Ask an Owner or Admin to change your role — do not try to “fix” the screen.
2. **Mode.** In Demo you are often signed in as a Viewer. Switch to Actual (with a live account) for real posting, or ask for a role that can post.
3. **No clinic yet.** Integrations and some settings stay empty until Ordo has set up this practice. Ask your office manager to email **[help@perfect.ventures](mailto:help@perfect.ventures)**.

---

## Related pages

- [EOB Dashboard](eob-dashboard.md)
- [Inside an EOB](working-an-eob.md)
- [Patients](patients.md)
- [Appointments](appointments.md)
- [Online booking page](online-booking.md)
- [Patient messages](patient-messages.md)
- [Analytics](analytics.md)
- [Clinic settings](clinic-settings.md)
- [Roles and who can do what](../people/roles.md)
